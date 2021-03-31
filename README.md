# wpf-code-rules

## Overview
- [WPF Core DLLs](#1-wpf-core-dlls)
- [Code Styles](#2-code-styles)
- [Try Catch](#3-try-catch)
- [Code Quality Check](#4-code-quality-check)
- [Resources](#5-resources)
<br />

### 1. WPF Core DLLs
- `System.Xaml`
- `WindowsBase`
- `PresentationCore`
- `PresentationFramework`
<br />

### 2. Code Styles
- [Property](#21-property)
- [Region](#22-region)

#### 2.1 Property
- __Property__
    ```csharp
    public string Email { get; set; }
    ```

- __Get Set Property__
    ```csharp
    private string _email;
    public string Email 
    { 
        get { return _email; } 
        set { _email = value; } 
    }
    ```
    __Be sure to name the `private` access restrictor for the variable.__

- __Observable Property__
    ```csharp
    private string _email;
    public string Email 
    { 
        get { return _email; } 
        set { _email = value; OnPropertyChanged(); } 
    }
    ```
    __Do not recommended to use `.base` for prefixes.__  
    :x: `base.OnPropertyChanged();` &nbsp;&nbsp; :heavy_check_mark: `OnPropertyChanged();`

- __Property with method in setter__
    ```csharp
    private string _email;
    public string Email 
    { 
        get { return _email; } 
        set { _email = value; OnPropertyChanged(); EmailChanged(value); } 
    }
    ```
<br />

#### 2.2 Region

```csharp
#region Email

private string _email;
public string Email
{
    get { return _email; }
    set { _email = value; OnPropertyChanged(); EmailChanged(value); }
}
#endregion
```
<br />

* * *

### 3. Try Catch

#### :exclamation: <ins>*Try Catch is generally not recommended.*</ins>  
Errors in the Try Catch area are not reflected in the program's operating cycle, which can cause application flow problems. To avoid this, it is not recommended to use Try Catch from the development stage.
<br />  
Especially, WPF applications that maintain organic flow to `.Xaml` and `.cs` and `Resource` areas have an advantage in not using Try Catch from the development stage.
It is recommended that you use a combination of __While__ statements to implement code that induces repetition of the Try Catch area and allows the user to control it.
<br />

#### :point_right: <ins>*Situation that Try Catch should be used*</ins>  
When you need to check __the success of the action__ through Try Catch.  
- `Local File Access`
- `Crawling`
- `API`  
- `External Connection`  
<br />

* * *

### 4. Code Quality Check

#### 4.1 Remove unused `xmlns:local`   
```xaml
<UserControl x:Class="TestProject.Views.TestUserControl"
             xmlns:local="clr-namespace:TestProject.Views;assembly=TestProject">
         ...
</UserControl>
```

#### 4.2 Decalre connected resource   
Check the location of the style resource in use and make sure it is properly declared in `App.xaml`.

#### 4.3 Classify each control style
Create styles of all controls to match each name rule.

#### 4.4 Remove unused `x:Name`      
Discard declared reckless name properties for access, such as `.cs` in View or ViewModel, and find a way to bypass them.

#### 4.5 Remove unused `using`

:point_right: __*Why we should remove unused `using`?*__  
- 가독성
- 불필요한 코드
- Namespace 중복, 충돌문제
- C# 객체지향 구조에 대한 이해도
<br />

* * *

### 5. Resources
> 'Resource Rules' is so important in WPF programs that you have to put more effort into than the program's UI design. Therefore, we would like to provide a guide to the main resources used by WPF in as much detail as possible.
#### Strong Name
Managing the resource system in a project is very complex and difficult. So, it is very important to abide by strict and strong naming rules from start to finish, and it requires continued patience.
#### Do not write without rules.
Temporarily creating resource without rules is a very bad way to develop them. This is because unmanaged resources accumulate, greatly hindering the readability and functional scalability of all program logic. Also, disorderly resources will continue to torment developers until the end of the program's life cycle. Therefore, it is important to make and maintain rules even if it is annoying at the time.
### Resource Types
  All UI objects inherited from the Visual class are subject to style classification.
- #### Style Classification Tree Structure
  - Visual
    - ContentControl
      - Button
      - ToggleButton
      - RadioButton
      - CheckBox
    - Control
      - TextBox
    - FrameworkElement
      - TextBlock
    - ItemsControl
      - ListBox (with ListBoxItem)
      - TreeView (with TreeViewItem)
  - Design
    - SolidBrush
    - Path
    - Geometry
    - Drawing   
  
* #### The reason for the detailed classification of styles.   
  If WPF properties are applied directly from the screen under development, source code readability, simplicity and quality can no longer be expected. Therefore, style rules and names should be intuitive and designed to infer functions and intentions.
* * *
### ContentControl
ContentControl that inherit FrameworkElement define names starting with **CTRL**.   
* #### Button   
  `TBD Image...`   
  Button controls are the most representative objects that use ControlTemplate simply and concisely.

  - #### Redirected / Namespace
    > *(**BTN**, System.Windows.Controls.**Button**)*   


  - #### Inheritance Class Flow
    > *Button > ButtonBase > ContentControl > Control > FrameworkElement > UIElement > Visual > DependencyObject*


  - #### Style Name Declaring
    The `x:Key` Property location is followed by the TargetType Property. 
    ```xaml
    <Style TargetType="{x:Type Button}" x:Key="CTRL.BTN.MAIN.OK"/>
    ```


  - #### Standard Style Struct with ControlTemplate
    WPF Button is a control that inherits ContentControl objects. Therefore, create a Style, including the ControlTemplate Property.
    ```xaml
    <Style Target="{x:Type Button}" x:Key="CTRL.BTN.MAIN.SIGNIN">
        <Setter Property="Background" Value="Transparent"/>
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="{x:Type Button}">
                    <Border Background="{TemplateParent Background}">
                        <ContentPresenter ContentSource="Content"/>
                    </Border>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
    ```
    > It is very important to specify the background of the control next to ControlTemplate. If you don't have a color to define, make sure to specify `Transparent`. In particular, for buttons, the scope of the Input event, such as `Click`, will be determined by the presence of this Background. So I usually use Border Control and Transparent Property.



* #### ToggleButton
  `TBD Image...`   
  TBD...
  - #### Redirected / Namespace
    > *(**TGL**, System.Windows.Controls.Primitives.**ToggleButton**)*   


  - #### Inheritance Class Flow
    > *ToggleButton > ButtonBase > ContentControl > Control > FrameworkElement > UIElement > Visual > DependencyObject*


  - #### Style Name Declaring
    The `x:Key` Property location is followed by the TargetType Property. 
    ```xaml
    <Style TargetType="{x:Type ToggleButton}" x:Key="CTRL.TGL.ACCOUNT.ON.OFF"/>
    ```


  - #### Standard Style Struct with ControlTemplate
    TBD...
    ```xaml
    <Style Target="{x:Type ToggleButton}" x:Key="CTRL.TGL.ACCOUNT.ON.OFF">
        <Setter Property="Background" Value="Transparent"/>
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="{x:Type ToggleButton}">
                    <Border Background="{TemplateParent Background}">
                        <ContentPresenter ContentSource="Content"/>
                    </Border>
                    <ControlTemplate.Triggers>
                        <Trigger Property="IsChecked" Value="True">
                            <Setter.Value Property="Background" Value="#EEEEEE"/>
                        </Trigger>
                    </ControlTemplate.Triggers>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
    ```
    > TBD...


* #### RadioButton
  `TBD Image...`   
  TBD..
  - #### Redirected / Namespace
    > *(**RDO**, System.Windows.Controls.**RadioButton**)*   


  - #### Inheritance Class Flow
    > *RadioButton > ToggleButton > ButtonBase > ContentControl > Control > FrameworkElement > UIElement > Visual > DependencyObject*


  - #### Style Name Declaring
    The `x:Key` Property location is followed by the TargetType Property. 
    ```xaml
    <Style TargetType="{x:Type RadioButton}" x:Key="CTRL.RDO.MAIN.HEADER"/>
    ```


  - #### Standard Style Struct with ControlTemplate
    TBD...



* #### CheckBox
  `TBD Image...`   
  TBD....
  - #### Redirected / Namespace
    > *(**CHK**, System.Windows.Controls.**CheckBox**)*   


  - #### Inheritance Class Flow
    > *CheckBox > ToggleButton > ButtonBase > ContentControl > Control > FrameworkElement > UIElement > Visual > DependencyObject*


  - #### Style Name Declaring
    The `x:Key` Property location is followed by the TargetType Property. 
    ```xaml
    <Style TargetType="{x:Type TextBox}" x:Key="CTRL.CHK.LOGIN.STAY"/>
    ```


  - #### Standard Style Struct with ControlTemplate
    TBD...


### FrameworkElement
TBD...

* #### TextBlock
  `TBD Image...`   
  TBD...
  - #### Redirected / Namespace
    > *(**TXB**, System.Windows.Controls.**TextBlock**)*   


  - #### Inheritance Class Flow
    > *TextBlock > FrameworkElement > UIElement > Visual > DependencyObject*


  - #### Style Name Declaring
    The `x:Key` Property location is followed by the TargetType Property. 
    ```xaml
    <Style TargetType="{x:Type TextBlock}" x:Key="CTRL.TXB.MAIN.HEADER"/>
    ```


  - #### Standard Style Struct with ControlTemplate
    TBD...


### Control
TBD...

* #### TextBox
  `TBD Image...`   
  TBD....
  - #### Redirected / Namespace
    > *(**TXT**, System.Windows.Controls.**TextBox**)*   


  - #### Inheritance Class Flow
    > *TextBox > TextBoxBase > Control > FrameworkElement > UIElement > Visual > DependencyObject*


  - #### Style Name Declaring
    The `x:Key` Property location is followed by the TargetType Property. 
    ```xaml
    <Style TargetType="{x:Type TextBox}" x:Key="CTRL.TXT.LOGIN.ID"/>
    ```


  - #### Standard Style Struct with ControlTemplate
    TBD..

### ItemsControl
TBD.....

* #### TreeView
  `TBD Image...`   
  TBD...
  - #### Redirected / Namespace
    > *(**TRV**, System.Windows.Controls.**TreeView**)*   


  - #### Inheritance Class Flow
    > *TreeView > ItemsControl > Control > FrameworkElement > UIElement > Visual > DependencyObject*


  - #### Style Name Declaring
    The `x:Key` Property location is followed by the TargetType Property. 
    ```xaml
    <Style TargetType="{x:Type TreeView}" x:Key="CTRL.TRV.MAIN.EXPLORER"/>
    ```


  - #### Standard Style Struct with ControlTemplate
    ```xaml
    <Style TargetType="{x:Type TreeViewItem}" x:Key="CTRL.TRVI.MAIN.EXPLORER">
       <!--- ??? --->
    </Style>

    <Style TargetType="{x:Type TreeView}" x:Key="CTRL.TRV.MAIN.EXPLORER">
        <Setter Property="ItemContainerStyle" Value="CTRL.TRVI.MAIN.EXPLORER"/>
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate/>
            <Setter.Value>
        </Setter>
    </Style>
    ```
    > What's unique here is that TreeView does not include ItemsPresenter in the Template, even though it inherits ItemsControl. This is an exceptional structure that the ItemsPresenter is included in TreeViewItem. Because, unlike other list-type controls, the data collection representation is hierarchy.



## 99. References
### Markdown
[Temp Link](https://docs.microsoft.com/en-us/windows/communitytoolkit/parsers/markdownparser)
TBD....
