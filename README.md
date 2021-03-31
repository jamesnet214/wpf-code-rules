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
It is recommended that you use a combination of __'While'__ statements to implement code that induces repetition of the Try Catch area and allows the user to control it.
<br />

#### :point_right: <ins>*Situation that Try Catch should be used*</ins>  
&nbsp; &nbsp; When you need to check *the success of the action* through Try Catch.  
- `Local File Access`
- `Crawling`
- `API`  
- `External Connection`  
<br />

* * *

### 4. Code Quality Check

#### View 단위별 체크
코드 품질 점검을 화면(View) 단위로 점검합니다.
- #### 코드 질 점검을 위한 세부 체크사항은 다음과 같습니다.   
  > 순서는 크게 상관이 없지만 각각의 체크항목의 개연성을 고려하여 순서가 정의되어 있습니다.   
  - #### View using 선언 확인   
    사용하지 않는 선언은 제거하도록 합니다.
    ### 예를들어:
    ```xaml
    <UserControl x:Class="TestProject.Views.TestUserControl1"
                 xmlns:local="clr-namespace:TestProject.Views;assembly=TestProject">
                 ...
    </UserControl>
    ```
    `xmlns:local` 선언을 실제 UserControl 영역에서 사용하고 있지 않는다면 바로 제거합니다. 그리고 향후 필요하다 하더라도 제거 후 나중에 추가하도록 합니다.
  - #### 연결된 Resource 확인   
    화면 전용 스타일 리소스 위치를 확인하고 `App.xaml`에 제대로 선언되어 있는지 확인합니다.
  - #### 각 컨트롤 Style 분류   
    모든 컨트롤은 각각의 이름 규칙에 맞게 스타일을 만들도록 합니다.
  - #### 무분별하게 남발된 `x:Name` 선언 부분 제거   
    View의 .cs 또는 ViewModel 등에서 접근하기 위해 선언된 무분별한 이름 속성들을 폐기하고 우회할 수 있는 방법을 찾도록 합니다.
  - #### .cs 사용하지 않는 using 제거
    사용하지 않는 using 문을 제거합니다. TBD...
    ### 굳이 using을 지워야 하는 이유:
    사요앟지 않는 using을 지우는 이유에는 여러가지가 있습니다.
    - #### 가독성
      TBD...
    - #### 불필요한 코드
      TBD...
    - #### Namespace 중복, 충돌문제
      TBD...
    - #### C# 객체지향 구조에 대한 이해도
      TBD...
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
