# wpfcoderules

## Get Started
## Overview
1. Property
2. Region
## Property Code Styles

### Property
```csharp
public string Email { get; set; }
```

### Get Set Property
```csharp
private string _email;
public string Email 
{ 
    get { return _email; } 
    set { _email = value; } 
}
```
Be sure to name the `private` access restrictor for the variable.
### Observable Property
```csharp
private string _email;
public string Email 
{ 
    get { return _email; } 
    set { _email = value; OnPropertyChanged(); } 
}
```
~base.OnPropertyChanged();~   
*Do not recommended to use `.base` for prefixes.*

### Property with method in setter
```csharp
private string _email;
public string Email 
{ 
    get { return _email; } 
    set { _email = value; Something(); OnPropertyChanged(); } 
}
```

## Region

### Region: Property
```csharp
#region Email

private string _email;
public string Email
{
    get { return _email; }
    set { _email = value; OnPropertyChanged(); }
}
#endregion
```

## 79. Bad Bindings
This is the Binding method that can be used in WPF.   

- Binding
- ElementName
- TemplateParent
- Self
- TemplatedParent
- AcensorType

> You can learn this technique in more detail here. [WPF Bindings](https://github.com/ncoresoftsource/wpfxamlbinding)

### Binding
TBD...
### ElementName
TBD...
Element Binding is a simple and easy-to-use Binding method. That is why this method is often overissued, affecting development pattern flow and readability.
- #### A bad example   
  ElementBinding can be used flexibly in various situations. However, it is not recommended to use it in the following situations.
  - ##### Do not use Bindings that exist in DataContext again through ElementBinding.
    > Using ElementBinding through connected control rather than using the Properties already declared in ViewModel is not a functional problem, but it breaks the fundamental pattern of Binding.   
    
    **Bad**
    ```xaml
    <TextBox x:Name="text" Text="{Binding UserName}"/>
    ...
    <TextBlock Text="{Binding ElementName=text, Path=Text}"/>
    ```
    
    **Good**   
    remove -> `x:Name="text"`
    ```xaml
    <!-- remove -> x:Name="text" -->
    <TextBox Text="{Binding UserName}"/>
    ...
    <TextBlock Text="{Binding UserName}"/>
    ```
  - ##### {RelativeSource Self}를 사용하여 계층 구조 형태로 Binding을 접근할 수 있는 상황에서 사용하지 마라.   
    **Bad**
    ```xaml
    <Window x:Name="win">
        <TextBlock Text="{Binding ElementName=win, Path=DataContext.UserName}"/>
        ...
    ```
    
    **Good**   
    remove -> `x:Name="win"`
    ```xaml
    <Window>
        <TextBlock Text="{Binding RelativeSource={RelativeSource AcensorType=Window}, Path=DataContext.UserName}"/>
        ...
    ```
    
    **Better Good**   
    ```xaml
    <Window>
        <TextBlock DataContext="{Binding RelativeSource={RelativeSource AcensorType=Window}, Path=DataContext}" Text="{Binding UserName"/>
        ...
    ```
  - ##### 계층구조 흐름을 거스르는 상황에서 ElementName을 사용하지 마라.
    TBD...

### TemplateParent
TBD...
### Self
TBD...
### TemplatedParent
TBD...
### AcensorType
TBD...

## 89. Resource Rules
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
  TBD...
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
  TBD...
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
  TBD...
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
    TBD...



### ItemsControl
TBD...

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
