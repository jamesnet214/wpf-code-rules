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

### Strong Name
Managing resource schemes in a project is very complex and difficult. That's why it's very important to adhere to strict and strong name rules, and it's a factor that needs to be taken from beginning to end. And it will be very hard. It requires patience and patience.

### 1. Controls
Controls that inherit FrmaeworkElement define names starting with **CTRL**.
   
* ### Button   
  > *(**BTN**, System.Windows.Controls.**Button**)*   
  
  #### Style Name Declaring
  The `x:Key` Property location is followed by the TargetType Property. 
  ```xaml
  <Style TargetType="{x:Type Button}" x:Key="CTRL.BTN.MAIN.OK"/>
  ```
  

  #### Standard Style Struct with ControlTemplate
  WPF Button is a control that inherits ContentControl objects. Therefore, create a Style, including the ControlTemplate Property.
  ```xaml
  <Style Target="{x:Type Button}" x:Key="CTRL.BTN.MAIN.SIGNIN">
      <Setter Property="Background" Value="Transparent"/>
      <Setter Property="Template">
          <Setter.Value>
              <ControlTemplate TargetType="{x:Type Button}">
                  <Border Background="{TemplateParent Background}">
                      <ContentPresenter/>
                  </Border>
              </ControlTemplate>
          </Setter.Value>
      </Setter>
  </Style>
  ```
  > It is very important to specify the background of the control next to ControlTemplate. If you don't have a color to define, make sure to specify a `Transparent`. In particular, for buttons, the scope of the Input event, such as clicking, will be determined by the presence of this Background. 'So I enjoy using Borders Control and Transparent Property`.

* **TXB**, System.Windows.Controls.**TextBlock**   

  ```xaml
  <Style TargetType="{x:Type TextBlock}" x:Key="CTRL.TXB.MAIN.HEADER"/>
  ```
  
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
  <Style TargetType="{x:Type ListBox}" x:Key="CTRL.LBXI.MAIN.USER"/>
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
