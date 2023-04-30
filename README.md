# Meetup WPF
- [블루포트](https://www.blueport.co.kr/Index.aspx)
- [인프라지스틱스](https://cafe.naver.com/infragisticskorea)
- [이재웅](https://github.com/jamesnet214)

## 이재웅
- [닷넷데브](https://dotnetdev.kr)
- [WPF 스터디](https://forum.dotnetdev.kr/t/wpf-3/6795)
- [유튜브 채널](https://youtube.com/@jamesnet214)
- [Jamesnet](https://jamesnet.dev)
- [WPF INSIDE OUT](https://jamesnet.dev/books) (책)
- [인스타그램](https://instagram.com/jamesnet214)
- [페이스북](https://facebook.com/jamesnet214)

## History
- 1회 3월 - 23일 목요일 (종료)
- 2회 4월 - 27일 목요일
- 3회 5월
- 4회 6월
- 5회 7월

## Content
- [x] 1. Project
- [x] 2. Reference
- [x] 3. Application
- [x] 4. Window
- [x] 5. StackPanel
- [x] 6. Grid
- [x] [7. IsHitTestVisible](#7-ishittestvisible)
- [x] 8. Border
- [x] 9. UniformGrid
- [x] 10. Visibility
- [x] 11. Opacity
- [x] 12. Transparent + Color
- [x] 13. Geometry
- [x] 14. DataContext
- [x] 15. Binding
- [x] 16. ViewModel
- [x] 17. Element Binding
- [x] [18. RelativeSource Binding](#18-relativesource-binding)
- [x] 19. Static Binding
- [x] 20. IValueConverter
- [x] 21. ResourceDictionary
--------------------------------------------------------------
- [X] [22. Button](#22-button)
- [X] [23. DataTemplate](#23-datatemplate)
- [X] 24. ControlTemplate**
- [X] 25. Trigger**
- [X] [26. ContentControl](#26-contentcontrol)
- [X] 27. ListBox**
- [X] 28. ListBoxItem**
--------------------------------------------------------------
- [ ] 29. **ItemsControl**
- [ ] 30. **CustomControl**
- [ ] 31. **GetContainerItemForOverride**
- [ ] 32. **AutoGrid.Core**
- [ ] 33. **CommunityToolkit**
- [ ] 34. **NugetPackage**
----------------------
- [ ] 35. Prism
- [ ] 36. Jamesnet.WPF

## 7. IsHitTestVisible

- 컨트롤이 겹쳐 있을 경우 최상위 컨트롤에서 설정하면 하위 컨트롤 클릭 가능 여부를 설정

| 설정 | 내용 | 
|:----|:----------|
| IsHitTestVisible="False" | 하위 컨트롤 클릭 가능 |
| IsHitTestVisible="True"  | 하위 컨트롤 클릭 불가 |

[목차](#content)

## 18. RelativeSource Binding

| 속성 | 내용 | 
|:----|:----------|
| AncestorType | 상위 컨트롤 중 참조할 항목 |
| AncestorLevel | 상위 컨트롤 참조할 항목 중 몇번째 인지 |
| Path | 어떤 속성의 값을 참조할 것인지? |

- 예시

| 구분 | 내용 | 
|:----|:----------|
| 예시구문1 | Text="{Binding RelativeSource={RelativeSource AncestorType=StackPanel, AncestorLevel=1}, Path=Background}" |
| 해석1 | 바로 상위에 있는 StackPanel의 배경색상을 참조할 것 |
| 예시구문2 | Text="{Binding RelativeSource={RelativeSource AncestorType=StackPanel, AncestorLevel=2}, Path=Background}" |
| 해석2 | 상위 두번째에 있는 StackPanel의 배경색상을 참조할 것 |

[목차](#content)

## 22. Button

- Style
- Style -> 복사본 편집
- Template -> ControlTemplate
- Trigger -> TargetType
- Content -> object
- Content -> ContentPresenter
- Button.Content -> 생략 가능

[목차](#content)

## 23. DataTemplate

- ContentControl을 상속 받는 클래스의 ContentTemplate을 재정의 해줌([26번 참조](#26-contentcontrol))
> `Content`를 재정의하고 있으며, `ContentControl`을 상속 받는 `Window`나 `Button`나 모두 같은 원리로 동작한다.

> `Button`, `ToggleButton`, `CheckBox`, `RadioButton` 등에 모두 같은 `DataTemplate`이 적용된 것을 볼 수 있다.

```xml
<!-- 아래화면의 xaml 코드 -->
    <Window.Resources>
        <DataTemplate x:Key="ButtonContentTemplate">
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="50"/>
                    <ColumnDefinition Width="70"/>
                </Grid.ColumnDefinitions>
                <TextBlock Grid.Row="0" Grid.Column="0" Text="Text1"/>
                <TextBlock Grid.Row="1" Grid.Column="1" Text="Text2"/>
            </Grid>
        </DataTemplate>
    </Window.Resources>
    <StackPanel Orientation="Horizontal" HorizontalAlignment="Left" VerticalAlignment="Top">
        <Button Margin="5"
                ContentTemplate="{StaticResource ButtonContentTemplate}"/>
        <ToggleButton Margin="5"
                  ContentTemplate="{StaticResource ButtonContentTemplate}"/>
        <CheckBox Margin="5"
                  ContentTemplate="{StaticResource ButtonContentTemplate}"/>
        <RadioButton Margin="5"
                     ContentTemplate="{StaticResource ButtonContentTemplate}"/>
    </StackPanel>
```

- 실행 화면

![DataTemplate Test](https://user-images.githubusercontent.com/72642836/235357755-1ed92831-42a2-4092-918c-9540b061420e.png)

[목차](#content)

## 24. ControlTemplate

- Template -> ControlTemplate
- Content -> ContentPresenter
- Trigger -> 주력 사용

## 25. Trigger

- Trigger -> TargetType 영향받음

## 26. ContentControl

- 컨트롤.Content -> 생략 가능

#### 26-1. ContentControl을 상속받는 개체와 아닌 개체의 차이점
1. ContentControl을 상속받는 개체
    -  주로 Content에 텍스트를 입력해서 사용하고 있는데, Content는 Object를 상속받고 있으므로, 사실 텍스트가 아닌 모든 것을 담을 수 있다.('Window'제외, image, ChekBox 등등)

|부모 클래스               |클래스|예시|
|:------------------------|:-----|:---|
|ContentControl >> ButtonBase|Button|`<Button Content="버튼"/>`|
|ContentControl >> ButtonBase|ToggleButton|상동(Content에 입력)|
|ContentControl >> ButtonBase >> ToggleButton|RadioButton|상동|
|ContentControl >> ButtonBase >> ToggleButton|CheckBox|상동|
|ContentControl >> HeaderedContentControl|TabItem|상동|
|ContentControl >> HeaderedContentControl|ToolBar|상동|
|ContentControl >> HeaderedContentControl|GroupBox|상동|
|ContentControl >> HeaderedContentControl|Expander|상동|
|ContentControl|ListBoxItem|상동|
|ContentControl >> ListBoxItem|ListViewItem|상동|
|ContentControl|Frame|상동|
|ContentControl|UserControl|상동|
|ContentControl|ScrolViewr|상동|
|ContentControl|Window|상동|
|ContentControl|TreeViewItem|상동|
|ContentControl|Label|상동|
|ContentControl|ComboBoxItem|상동|

2. 이 외의 객체
    - ConTentControl을 상속 받는 개체와 달리 아래 항목은 Text만 담을 수 있다.

|부모 클래스               |클래스|예시|
|:------------------------|:-----|:---|
|FrameworkElement|TextBlock|`<TextBlock Text="텍스트블록">`|
|TextBoxBase|TextBox|`<TextBox Text="텍스트박스">`|

[목차](#content)

## 27. ListBox

TBD...

## 28. ListBoxItem

TBD...

## 29. ItemsControl

TBD...

## 30. CustomControl

TBD...

## 31. GetContainerItemForOverride

TBD...

## 32. AutoGrid.Core

TBD...

## 33. CommunityToolkit

TBD...

## 34. NugetPackage

TBD...
