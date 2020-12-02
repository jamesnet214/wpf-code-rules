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
### 1. Controls
Controls that inherit FrmaeworkElement define names starting with **CTRL**.
   
* Button
  - Style `x:Key` Rules   
**BTN**, System.Windows.Controls.**Button**   
+ ```xaml
  <Style TargetType="{x:Type Button}" x:Key="CTRL.BTN.MAIN.OK"/>
  ```

    + Basic ControlTemplate
  ```xaml
  <Style Target="{x:Type Button}" x:Key="CTRL.BTN.MAIN.SIGNIN">
      <Setter Property="">
          <Setter.Value>
              <ControlTemplate TargetType="{x:Type Button}">
          </Setter.Value>
      </Setter>
  </Style>
  ```

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

## 99. References
### Markdown
[Temp Link](https://docs.microsoft.com/en-us/windows/communitytoolkit/parsers/markdownparser)
