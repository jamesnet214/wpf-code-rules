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

## 89. Resource Rules
'Resource Rules' is so important in WPF programs that you have to put more effort into than the program's UI design. Therefore, we would like to provide a guide to the main resources used by WPF in as much detail as possible.
### Strong Name
Managing the resource system in a project is very complex and difficult. So, it is very important to abide by strict and strong naming rules from start to finish, and it requires continued patience.
### Do not write without rules.
Temporarily creating resource without rules is a very bad way to develop them. This is because unmanaged resources accumulate, greatly hindering the readability and functional scalability of all program logic. Also, disorderly resources will continue to torment developers until the end of the program's life cycle. Therefore, it is important to make and maintain rules even if it is annoying at the time.
### 1. Controls
    Controls that inherit FrameworkElement define names starting with **CTRL**.
   
* ### Button   
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
  
  
  
* ### ToggleButton
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
  
  
  
* ### TextBlock
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
  


* ### TextBox
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
  


* ### CheckBox
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
  
  
* **TRV**, System.Windows.Controls.**TreeView**   

  ```xaml
  <Style TargetType="{x:Type TreeView}" x:Key="CTRL.TRV.MAIN.EXPLORER"/>
  ```
  
* **TRVI**, System.Windows.Controls.**TreeViewItem**   

  ```xaml
  <Style TargetType="{x:Type TreeViewItem}" x:Key="CTRL.TRVI.MAIN.EXPLORER"/>
  ```
  
* **LBX**, System.Windows.Controls.**ListBox**   

  ```xaml
  <Style TargetType="{x:Type ListBox}" x:Key="CTRL.LBX.MAIN.USER"/>
  ```
  
* **LBXI**, System.Windows.Controls.**ListBoxItem**   

  ```xaml
  <Style TargetType="{x:Type ListBoxItem}" x:Key="CTRL.LBXI.MAIN.USER"/>
  ```
  
* **IMG**, System.Windows.Controls.**Image**

  ```xaml
  <Style TargetType="{x:Type Image}" x:Key="CTRL.IMG.MAIN.USER"/>
  ```
  

## 99. References
### Markdown
[Temp Link](https://docs.microsoft.com/en-us/windows/communitytoolkit/parsers/markdownparser)
