## WPF Code Rules
  
이 레포지토리는 체계적인 프로젝트 구조 생성을 위한 WPF 코드 규칙에 대해 설명하고 있습니다. <br />

<a href="https://github.com/devncore/devncore"><strong>더 알아보기 »</strong></a>
  
| Star | License | Activity |
|:----:|:-------:|:--------:|
| <a href="https://github.com/devncore/wpf-code-rules/stargazers"><img src="https://img.shields.io/github/stars/devncore/wpf-code-rules" alt="Github Stars"></a> | <img src="https://img.shields.io/github/license/devncore/wpf-code-rules" alt="License"> | <a href="https://github.com/devncore/wpf-code-rules/pulse"><img src="https://img.shields.io/github/commit-activity/m/devncore/wpf-code-rules" alt="Commits-per-month"></a> |

<br />

## 소개
- [핵심 DLL](#핵심-dll)
- [코드 스타일](#코드-스타일)
- [Try Catch](#try-catch)
- [코드 품질 체크](#코드-품질-체크)
- [Resources](#resources)
 
<br />

## 핵심 DLL
- `System.Xaml`
- `WindowsBase`
- `PresentationCore`
- `PresentationFramework`
<br />

## 코드 스타일

#### Property
  ```csharp
  public string Email { get; set; }
  ```

#### Get Set Property
```csharp
private string _email;
public string Email 
{ 
    get { return _email; } 
    set { _email = value; } 
}
```

#### Observable Property
```csharp
private string _email;
public string Email 
{ 
    get { return _email; } 
    set { _email = value; OnPropertyChanged(); } 
}
```
__`base`를 사용하는 것은 추천하지 않습니다.__   

❌ `base.OnPropertyChanged();` &nbsp;&nbsp; ✔️ `OnPropertyChanged();`

#### Property with method in setter
```csharp
private string _email;
public string Email 
{ 
    get { return _email; } 
    set { _email = value; OnPropertyChanged(); EmailChanged(value); } 
}
```
    
#### Region

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

## Try Catch

#### ❗ <ins>*Try Catch의 사용은 추천하지 않습니다.*</ins>  
Try Catch 영역에서 일어난 에러들은 프로그램 작동 주기에 반영되지 않기 때문에 응용 프로그램 흐름 문제를 발생시킬 수 있습니다. 이러한 문제를 방지하려면 개발 단계부터 Try Catch를 사용하지 않는 것이 좋습니다.

특히 `xaml`과 `cs`, 리소스 영역 간 유기적인 흐름을 유지하는 WPF 애플리케이션은 개발 단계부터 Try Catch를 사용하지 않을 때 더욱 큰 이점을 가집니다. Try Catch 영역의 반복을 유도하고 사용자가 제어할 수 있는 코드를 구현하려면 **While**문을 조합하여 사용하는 것이 좋습니다.
<br />

#### 👉 <ins>*Try Catch를 반드시 사용해야 하는 경우*</ins>  
특정 행위의 성공 여부를 체크해야 할 때는 Try Catch를 사용하는 것이 좋습니다.  
- 로컬 파일 접근  
- 크롤링  
- 외부 연결
- API  
<br />

## 코드 품질 체크

#### ◾ 사용하지 않는 `xmlns:local` 제거   
```xaml
<UserControl x:Class="TestProject.Views.TestUserControl"
             xmlns:local="clr-namespace:TestProject.Views;assembly=TestProject">
         ...
</UserControl>
```

#### ◾ 연결된 리소스 명시   
사용중인 스타일 리소스의 위치를 확인하고 `App.xaml`에 적절히 선언되었는지 확인합니다.

#### ◾ 각 컨트롤 스타일의 분류
컨트롤들의 스타일은 각각의 네이밍 규칙에 맞춰 생성합니다.

#### ◾ 사용하지 않는 `x:Name` 제거      
View 또는 ViewModel의 `.cs` 접근을 위해 선언된 `x:Name`들을 삭제하고 이를 대체할 방법을 찾습니다.

#### ◾ 사용하지 않는 `using` 제거
- 가독성
- 불필요한 코드
- 네임스페이스의 불필요한 반복과 충돌 이슈
- C#의 객체지향 구조에 대한 이해
<br />

## Resources
*WPF 프로그램에서 **리소스 규칙**은 매우 중요하기 때문에 프로그램의 UI 설계보다 더 많은 노력을 기울여야 합니다. 따라서 WPF에서 사용하는 주요 리소스에 대한 가이드를 최대한 상세하게 제공하고자 합니다.*

프로젝트에서 리소스 시스템을 관리하는 것은 매우 복잡하고 어렵습니다. 그래서 처음부터 끝까지 엄격하고 **강력한 네이밍 규칙**을 지키는 것이 매우 중요하며, 이는 지속적인 인내를 필요로 합니다.

리소스들을 정해진 규칙 없이 일시적으로 생성하는 것은 매우 나쁜 방법입니다. 이는 관리되지 않는 리소스들이 축적되어 모든 프로그램 로직의 가독성과 기능적 확장성을 크게 방해하기 때문입니다. 또한, 무질서한 리소스는 프로그램의 생명 주기가 끝날 때까지 개발자들을 계속 괴롭힐 것입니다. 그렇기 때문에 약간 귀찮더라도 규칙을 만들고 유지하는 것이 중요합니다.

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

