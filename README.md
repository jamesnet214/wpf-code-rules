# wpf-code-rules
### About us

> &nbsp; :adult: __James Lee__ &nbsp;&nbsp; [Github](https://github.com/devncore-james) &nbsp;&nbsp; james.lee@devncore.org  
> &nbsp; :woman: __Elena Kim__ &nbsp;&nbsp; [Github](https://github.com/devncore-elena) &nbsp;&nbsp; elena.kim@devncore.org

We are very ordinary developers, so we need to communicate with you.   
You can always share information with us and we are looking forward to it.  

##### _Open Source &nbsp; https://github.com/devncore/devncore   &nbsp;&nbsp;   Official Website &nbsp; https://devncore.org_ 

### License Policy
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

***

## Overview
- [WPF Core DLLs](#wpf-core-dlls)
- [Code Styles](#code-styles)
- [Try Catch](#try-catch)
- [Code Quality Check](#code-quality-check)
- [Resources](#resources)
<br />

## WPF Core DLLs
- `System.Xaml`
- `WindowsBase`
- `PresentationCore`
- `PresentationFramework`
<br />

## Code Styles
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

## Try Catch

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

## Code Quality Check

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

:point_right: __*Why we should remove unused `using`? (TBD...)*__  
- Readability
- Unnecessary code
- Namespace redundancy, conflict issues
- Understanding of object-oriented structures of C#
<br />

* * *

## Resources

*__Resource Rule__ is so important in WPF programs that you have to put more effort into than the program's UI design. Therefore, we would like to provide a guide to the main resources used by WPF in as much detail as possible.*

#### :exclamation: Strong Name
Managing the resource system in a project is very complex and difficult. So, it is very important to abide by strict and strong naming rules from start to finish, and it requires continued patience.

#### :exclamation: Do not write without rules.
Temporarily creating resource without rules is a very bad way to develop them. This is because unmanaged resources accumulate, greatly __hindering the readability and functional scalability of all program logic__. Also, disorderly resources will continue to torment developers until the end of the program's life cycle. Therefore, it is important to make and maintain rules even if it is annoying at the time.

#### Style Classification Tree Structure
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
  
    #### :point_right: The reason for the detailed classification of styles.   
    &nbsp; If WPF properties are applied directly from the screen under development, source code readability, simplicity and quality can no longer be expected. Therefore, style rules and names should be intuitive and designed to infer functions and intentions.
<br />

#### ContentControl

|Control|Naming|Namespace|Inheritance Flow|
|:-----:|:----:|:--------|:---------------|
|**Button**      |**BTN**|System.Windows.Controls |_Button > ButtonBase > ContentControl > Control > FrameworkElement > UIElement > Visual > DependencyObject_|
|**ToggleButton**|**TGL**|System.Windows.Controls.Primitives |_ToggleButton > ButtonBase > ContentControl > Control > FrameworkElement > UIElement > Visual > DependencyObject_|
|**RadioButton** |**RDO**|System.Windows.Controls |_RadioButton > ToggleButton > ButtonBase > ContentControl > Control > FrameworkElement > UIElement > Visual > DependencyObject_|
|**CheckBox**    |**CHB**|System.Windows.Controls |_CheckBox > ToggleButton > ButtonBase > ContentControl > Control > FrameworkElement > UIElement > Visual > DependencyObject_|

<br />

#### Control

|Control|Naming|Namespace|Inheritance Flow|
|:-----:|:----:|:--------|:---------------|
|**TextBox**|**TXT**|System.Windows.Controls|_TextBox > TextBoxBase > Control > FrameworkElement > UIElement > Visual > DependencyObject_|

<br />

#### FrameworkElement

|Control|Naming|Namespace, Inheritance Flow|
|:-----:|:----:|:---------------|
|**TextBlock**|**TXB**| :black_medium_small_square: **System.Windows.Controls**<br/> :white_medium_small_square: _TextBlock > FrameworkElement > UIElement > Visual > DependencyObject_|

<br />

#### ItemsControl

|Control|Naming|Namespace|Inheritance Flow|
|:-----:|:----:|:--------|:---------------|
|**ListBox** |**LBX**|System.Windows.Controls |_ListBox > Selector > ItemsControl > Control > FrameworkElement > UIElement > Visual > DependencyObject_|
|**TreeView**|**TRV**|System.Windows.Controls|_TreeView > ItemsControl > Control > FrameworkElement > UIElement > Visual > DependencyObject_|

<br />

## 99. References

### Markdown
- [Temp Link](https://docs.microsoft.com/en-us/windows/communitytoolkit/parsers/markdownparser)

- [the-easiest-markdown](https://github.com/devncore/the-easiest-markdown)
