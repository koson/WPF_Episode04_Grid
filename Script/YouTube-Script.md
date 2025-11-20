# สคริปต์การสอน: WPF Episode 04 - Grid Layout

## เนื้อหาที่จะสอน

### 1. Grid คืออะไร
- Grid เป็น Layout Panel ที่ทรงพลังที่สุดใน WPF
- ใช้สร้าง Layout แบบ Row และ Column คล้าย Table

### 2. การใช้งาน Grid
- RowDefinitions และ ColumnDefinitions
- Grid.Row และ Grid.Column
- Grid.RowSpan และ Grid.ColumnSpan

### 3. สร้าง Calculator App
- ใช้ Grid สร้างเครื่องคิดเลขจริง

---

## ส่วนที่ 1: Introduction (0:00 - 2:00)

**สวัสดีครับทุกคน**

ยินดีต้อนรับกลับมาสู่ WPF Tutorial Series ของเรา

วันนี้เราจะมาเรียนรู้เกี่ยวกับ **Grid** ซึ่งเป็น Layout Panel ที่ทรงพลังที่สุดและใช้บ่อยที่สุดใน WPF

Grid เป็นเหมือน Table ที่เรารู้จักครับ มี Row (แถว) และ Column (คอลัมน์) 
เราสามารถวาง Control ต่างๆ ลงในช่อง (Cell) ต่างๆ ได้

และวันนี้เราจะสร้าง **Calculator App** จริงๆ ด้วย Grid นะครับ!

---

## ส่วนที่ 2: Grid พื้นฐาน (2:00 - 8:00)

### Demo 2.1: Grid เปล่าๆ

เริ่มต้นด้วย Grid เปล่าๆ ก่อน

```xml
<Grid>
</Grid>
```

Grid เปล่าๆ จะมี 1 Row และ 1 Column เป็น default

### Demo 2.2: เพิ่ม Button ใน Grid

ลองใส่ Button เข้าไปดู

```xml
<Grid>
    <Button Content="Click Me"/>
</Grid>
```

**สังเกตไหมครับ:** Button จะยืดเต็ม Grid เลย

เพราะ default ของ `HorizontalAlignment` และ `VerticalAlignment` คือ `Stretch`

### Demo 2.3: กำหนดขนาด Button

ถ้าเราต้องการให้ Button มีขนาดเฉพาะ

```xml
<Grid>
    <Button Content="Click Me" 
            Width="100" 
            Height="40"/>
</Grid>
```

ตอนนี้ Button จะอยู่ตรงกลาง (Center) และมีขนาดตามที่กำหนด

---

## ส่วนที่ 3: RowDefinitions และ ColumnDefinitions (8:00 - 15:00)

### Demo 3.1: สร้าง 2 Rows

ถ้าเราต้องการหลาย Rows ต้องกำหนดด้วย `RowDefinitions`

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Button Grid.Row="0" Content="Row 0"/>
    <Button Grid.Row="1" Content="Row 1"/>
</Grid>
```

**อธิบาย:**
- `<Grid.RowDefinitions>` - บอกว่าจะมีกี่ Row
- `<RowDefinition/>` - กำหนดแต่ละ Row
- `Grid.Row="0"` - บอกว่า Element นี้อยู่ Row ไหน (เริ่มจาก 0)

### Demo 3.2: สร้าง 3 Columns

ตอนนี้มาลองสร้าง Columns บ้าง

```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition/>
        <ColumnDefinition/>
        <ColumnDefinition/>
    </Grid.ColumnDefinitions>
    
    <Button Grid.Column="0" Content="Col 0"/>
    <Button Grid.Column="1" Content="Col 1"/>
    <Button Grid.Column="2" Content="Col 2"/>
</Grid>
```

**อธิบาย:**
- `<Grid.ColumnDefinitions>` - บอกว่าจะมีกี่ Column
- `<ColumnDefinition/>` - กำหนดแต่ละ Column
- `Grid.Column="0"` - บอกว่า Element นี้อยู่ Column ไหน

### Demo 3.3: ทั้ง Rows และ Columns

ตอนนี้ลองรวมกันดู สร้าง Grid 2x3 (2 Rows, 3 Columns)

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Grid.ColumnDefinitions>
        <ColumnDefinition/>
        <ColumnDefinition/>
        <ColumnDefinition/>
    </Grid.ColumnDefinitions>
    
    <!-- Row 0 -->
    <Button Grid.Row="0" Grid.Column="0" Content="0,0"/>
    <Button Grid.Row="0" Grid.Column="1" Content="0,1"/>
    <Button Grid.Row="0" Grid.Column="2" Content="0,2"/>
    
    <!-- Row 1 -->
    <Button Grid.Row="1" Grid.Column="0" Content="1,0"/>
    <Button Grid.Row="1" Grid.Column="1" Content="1,1"/>
    <Button Grid.Row="1" Grid.Column="2" Content="1,2"/>
</Grid>
```

**เห็นไหมครับ:** ตอนนี้เรามี Table 2x3 แล้ว!

---

## ส่วนที่ 4: กำหนดขนาด Row และ Column (15:00 - 22:00)

### 4.1 Width และ Height Properties

มี 3 แบบในการกำหนดขนาด:

1. **Auto** - ขนาดตามเนื้อหา
2. **Fixed** (เช่น 100) - ขนาดคงที่ (pixels)
3. **Star (*)** - แบ่งพื้นที่ที่เหลือ

### Demo 4.1: Auto Size

```xml
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="Auto"/>
    <ColumnDefinition Width="Auto"/>
</Grid.ColumnDefinitions>
```

Column จะกว้างพอดีกับเนื้อหา

### Demo 4.2: Fixed Size

```xml
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="100"/>
    <ColumnDefinition Width="200"/>
</Grid.ColumnDefinitions>
```

Column แรก 100 pixels, Column ที่สอง 200 pixels

### Demo 4.3: Star Size (*)

**นี่สำคัญมากครับ!** Star (*) คือการแบ่งพื้นที่แบบ Proportional

```xml
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="*"/>
    <ColumnDefinition Width="*"/>
</Grid.ColumnDefinitions>
```

ทั้ง 2 Column จะแบ่งพื้นที่เท่าๆ กัน (50%-50%)

### Demo 4.4: Star Size with Ratio

```xml
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="2*"/>
    <ColumnDefinition Width="*"/>
</Grid.ColumnDefinitions>
```

Column แรกจะได้ 2 ส่วน, Column ที่สองได้ 1 ส่วน
คิดเป็น 66.67% : 33.33%

### Demo 4.5: ผสมกัน

```xml
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="Auto"/>
    <ColumnDefinition Width="100"/>
    <ColumnDefinition Width="*"/>
    <ColumnDefinition Width="2*"/>
</Grid.ColumnDefinitions>
```

- Column 0: ตามเนื้อหา
- Column 1: 100 pixels
- Column 2: 1 ส่วนของที่เหลือ
- Column 3: 2 ส่วนของที่เหลือ

---

## ส่วนที่ 5: Margin และ Padding (22:00 - 25:00)

### Demo 5.1: Margin

Margin คือระยะห่างด้านนอก Element

```xml
<Button Grid.Row="0" Grid.Column="0" 
        Content="Button" 
        Margin="10"/>
```

Margin 10 pixels ทุกด้าน

### Demo 5.2: Margin แต่ละด้าน

```xml
<Button Margin="10,5,10,5"/>
<!-- Left, Top, Right, Bottom -->
```

หรือ

```xml
<Button Margin="10,5"/>
<!-- Horizontal, Vertical -->
```

### Demo 5.3: Margin สำหรับทั้ง Grid

```xml
<Grid Margin="20">
    <!-- Content here -->
</Grid>
```

ทั้ง Grid จะห่างจากขอบ Window 20 pixels

---

## ส่วนที่ 6: สร้าง Calculator - ขั้นตอนที่ 1 (25:00 - 30:00)

ตอนนี้เรามาสร้าง Calculator กันเลยครับ!

### Demo 6.1: โครงสร้างหลัก

Calculator ของเราจะมี 2 ส่วน:
1. หน้าจอแสดงผล (บนสุด)
2. ปุ่มกด (ด้านล่าง)

```xml
<Grid Margin="20">
    <Grid.RowDefinitions>
        <RowDefinition Height="60"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
</Grid>
```

**อธิบาย:**
- Row 0: สูง 60 pixels สำหรับหน้าจอ
- Row 1: เต็มพื้นที่ที่เหลือ (*) สำหรับปุ่ม

### Demo 6.2: เพิ่มหน้าจอแสดงผล

```xml
<TextBox Grid.Row="0" 
         Text="0" 
         FontSize="32" 
         TextAlignment="Right" 
         VerticalContentAlignment="Center" 
         Padding="10"/>
```

**อธิบาย Properties:**
- `Grid.Row="0"` - อยู่แถวบนสุด
- `Text="0"` - แสดงเลข 0
- `FontSize="32"` - ตัวอักษรใหญ่
- `TextAlignment="Right"` - ข้อความชิดขวา (เหมือนเครื่องคิดเลขจริง)
- `VerticalContentAlignment="Center"` - ข้อความอยู่ตรงกลางแนวตั้ง
- `Padding="10"` - ระยะห่างด้านใน

---

## ส่วนที่ 7: สร้าง Calculator - ขั้นตอนที่ 2 (30:00 - 40:00)

### Demo 7.1: Grid สำหรับปุ่ม

ปุ่มของ Calculator เราจะเป็น Grid 4x4 (4 Rows, 4 Columns)

```xml
<Grid Grid.Row="1" Margin="0,10,0,0">
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Grid.ColumnDefinitions>
        <ColumnDefinition/>
        <ColumnDefinition/>
        <ColumnDefinition/>
        <ColumnDefinition/>
    </Grid.ColumnDefinitions>
</Grid>
```

**อธิบาย:**
- ใช้ `Grid.Row="1"` เพราะอยู่ Row ที่ 2
- `Margin="0,10,0,0"` ให้ห่างจากหน้าจอด้านบน 10 pixels
- 4 Rows และ 4 Columns ทั้งหมดใช้ `*` (แบ่งเท่าๆ กัน)

### Demo 7.2: แถวแรก (7, 8, 9, ÷)

```xml
<!-- Row 0 -->
<Button Grid.Row="0" Grid.Column="0" Content="7" FontSize="24" Margin="2"/>
<Button Grid.Row="0" Grid.Column="1" Content="8" FontSize="24" Margin="2"/>
<Button Grid.Row="0" Grid.Column="2" Content="9" FontSize="24" Margin="2"/>
<Button Grid.Row="0" Grid.Column="3" Content="/" FontSize="24" Margin="2" Background="#FFE0A0"/>
```

**อธิบาย:**
- `Grid.Row="0"` - แถวแรก
- `Grid.Column="0,1,2,3"` - แต่ละคอลัมน์
- `FontSize="24"` - ตัวเลขใหญ่
- `Margin="2"` - ห่างกัน 2 pixels
- `Background="#FFE0A0"` - สีพื้นหลัง (สีส้มอ่อนสำหรับปุ่มคำนวณ)

### Demo 7.3: แถวที่สอง (4, 5, 6, ×)

```xml
<!-- Row 1 -->
<Button Grid.Row="1" Grid.Column="0" Content="4" FontSize="24" Margin="2"/>
<Button Grid.Row="1" Grid.Column="1" Content="5" FontSize="24" Margin="2"/>
<Button Grid.Row="1" Grid.Column="2" Content="6" FontSize="24" Margin="2"/>
<Button Grid.Row="1" Grid.Column="3" Content="*" FontSize="24" Margin="2" Background="#FFE0A0"/>
```

### Demo 7.4: แถวที่สาม (1, 2, 3, −)

```xml
<!-- Row 2 -->
<Button Grid.Row="2" Grid.Column="0" Content="1" FontSize="24" Margin="2"/>
<Button Grid.Row="2" Grid.Column="1" Content="2" FontSize="24" Margin="2"/>
<Button Grid.Row="2" Grid.Column="2" Content="3" FontSize="24" Margin="2"/>
<Button Grid.Row="2" Grid.Column="3" Content="-" FontSize="24" Margin="2" Background="#FFE0A0"/>
```

### Demo 7.5: แถวสุดท้าย (C, 0, =, +)

```xml
<!-- Row 3 -->
<Button Grid.Row="3" Grid.Column="0" Content="C" FontSize="24" Margin="2" Background="#FFA0A0"/>
<Button Grid.Row="3" Grid.Column="1" Content="0" FontSize="24" Margin="2"/>
<Button Grid.Row="3" Grid.Column="2" Content="=" FontSize="24" Margin="2" Background="#A0FFA0"/>
<Button Grid.Row="3" Grid.Column="3" Content="+" FontSize="24" Margin="2" Background="#FFE0A0"/>
```

**อธิบาย:**
- `Background="#FFA0A0"` - สีแดงอ่อนสำหรับปุ่ม Clear
- `Background="#A0FFA0"` - สีเขียวอ่อนสำหรับปุ่ม =
- `Background="#FFE0A0"` - สีส้มอ่อนสำหรับปุ่มคำนวณ

---

## ส่วนที่ 8: รวมโค้ดทั้งหมด (40:00 - 42:00)

### Code Complete

```xml
<Page x:Class="WpfAppEX04.GridDemo" 
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" 
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" 
      Title="Grid Demo">
    <Grid Margin="20">
        <Grid.RowDefinitions>
            <RowDefinition Height="60"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
        
        <!-- Display -->
        <TextBox Grid.Row="0" 
                 Text="0" 
                 FontSize="32" 
                 TextAlignment="Right" 
                 VerticalContentAlignment="Center" 
                 Padding="10"/>
        
        <!-- Buttons -->
        <Grid Grid.Row="1" Margin="0,10,0,0">
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            
            <!-- Row 0: 7 8 9 / -->
            <Button Grid.Row="0" Grid.Column="0" Content="7" FontSize="24" Margin="2"/>
            <Button Grid.Row="0" Grid.Column="1" Content="8" FontSize="24" Margin="2"/>
            <Button Grid.Row="0" Grid.Column="2" Content="9" FontSize="24" Margin="2"/>
            <Button Grid.Row="0" Grid.Column="3" Content="/" FontSize="24" Margin="2" Background="#FFE0A0"/>
            
            <!-- Row 1: 4 5 6 * -->
            <Button Grid.Row="1" Grid.Column="0" Content="4" FontSize="24" Margin="2"/>
            <Button Grid.Row="1" Grid.Column="1" Content="5" FontSize="24" Margin="2"/>
            <Button Grid.Row="1" Grid.Column="2" Content="6" FontSize="24" Margin="2"/>
            <Button Grid.Row="1" Grid.Column="3" Content="*" FontSize="24" Margin="2" Background="#FFE0A0"/>
            
            <!-- Row 2: 1 2 3 - -->
            <Button Grid.Row="2" Grid.Column="0" Content="1" FontSize="24" Margin="2"/>
            <Button Grid.Row="2" Grid.Column="1" Content="2" FontSize="24" Margin="2"/>
            <Button Grid.Row="2" Grid.Column="2" Content="3" FontSize="24" Margin="2"/>
            <Button Grid.Row="2" Grid.Column="3" Content="-" FontSize="24" Margin="2" Background="#FFE0A0"/>
            
            <!-- Row 3: C 0 = + -->
            <Button Grid.Row="3" Grid.Column="0" Content="C" FontSize="24" Margin="2" Background="#FFA0A0"/>
            <Button Grid.Row="3" Grid.Column="1" Content="0" FontSize="24" Margin="2"/>
            <Button Grid.Row="3" Grid.Column="2" Content="=" FontSize="24" Margin="2" Background="#A0FFA0"/>
            <Button Grid.Row="3" Grid.Column="3" Content="+" FontSize="24" Margin="2" Background="#FFE0A0"/>
        </Grid>
    </Grid>
</Page>
```

**ดูสวยงามมั้ยครับ!** เราได้ Calculator ที่ดูเหมือนของจริงแล้ว!

---

## ส่วนที่ 9: Grid.RowSpan และ Grid.ColumnSpan (42:00 - 47:00)

### 9.1 RowSpan คืออะไร

RowSpan ใช้เมื่อต้องการให้ Element ขยายข้าม หลาย Rows

### Demo 9.1: RowSpan Example

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Grid.ColumnDefinitions>
        <ColumnDefinition/>
        <ColumnDefinition/>
    </Grid.ColumnDefinitions>
    
    <Button Grid.Row="0" Grid.Column="0" Content="Normal"/>
    <Button Grid.Row="0" Grid.Column="1" 
            Grid.RowSpan="3" 
            Content="RowSpan=3" 
            Background="LightBlue"/>
</Grid>
```

**อธิบาย:**
- Button ที่สองขยายข้าม 3 Rows (Row 0, 1, 2)

### 9.2 ColumnSpan คืออะไร

ColumnSpan ใช้เมื่อต้องการให้ Element ขยายข้าม หลาย Columns

### Demo 9.2: ColumnSpan Example

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Grid.ColumnDefinitions>
        <ColumnDefinition/>
        <ColumnDefinition/>
        <ColumnDefinition/>
    </Grid.ColumnDefinitions>
    
    <Button Grid.Row="0" Grid.Column="0" 
            Grid.ColumnSpan="3" 
            Content="ColumnSpan=3" 
            Background="LightGreen"/>
    <Button Grid.Row="1" Grid.Column="0" Content="Col 0"/>
    <Button Grid.Row="1" Grid.Column="1" Content="Col 1"/>
    <Button Grid.Row="1" Grid.Column="2" Content="Col 2"/>
</Grid>
```

**อธิบาย:**
- Button ที่หนึ่งขยายข้าม 3 Columns

### Demo 9.3: ทั้ง RowSpan และ ColumnSpan

```xml
<Button Grid.Row="1" Grid.Column="1" 
        Grid.RowSpan="2" Grid.ColumnSpan="2" 
        Content="Big Button" 
        Background="Yellow"/>
```

Button จะขยายข้าม 2 Rows และ 2 Columns!

---

## ส่วนที่ 10: Tips & Best Practices (47:00 - 50:00)

### 10.1 การตั้งชื่อที่ดี

```xml
<!-- ไม่ดี -->
<Grid>
    <Button Grid.Row="0" Grid.Column="0" Content="OK"/>
</Grid>

<!-- ดี -->
<Grid x:Name="MainGrid">
    <Button x:Name="OkButton" Grid.Row="0" Grid.Column="0" Content="OK"/>
</Grid>
```

### 10.2 ใช้ Margin อย่างสม่ำเสมอ

```xml
<!-- แทนที่จะใช้ Margin แยกทุก Element -->
<Button Margin="5"/>
<Button Margin="5"/>
<Button Margin="5"/>

<!-- ใช้ Style ดีกว่า -->
<Grid.Resources>
    <Style TargetType="Button">
        <Setter Property="Margin" Value="5"/>
        <Setter Property="FontSize" Value="24"/>
    </Style>
</Grid.Resources>
```

### 10.3 Nested Grid

Grid สามารถซ้อนกันได้ เพื่อสร้าง Layout ที่ซับซ้อน

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    
    <!-- Header -->
    <Grid Grid.Row="0" Background="Navy">
        <TextBlock Text="Header" Foreground="White"/>
    </Grid>
    
    <!-- Content Area -->
    <Grid Grid.Row="1">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="200"/>
            <ColumnDefinition Width="*"/>
        </Grid.ColumnDefinitions>
        
        <!-- Sidebar -->
        <Grid Grid.Column="0" Background="LightGray">
            <!-- Sidebar content -->
        </Grid>
        
        <!-- Main Content -->
        <Grid Grid.Column="1">
            <!-- Main content -->
        </Grid>
    </Grid>
</Grid>
```

### 10.4 Performance Tips

- ใช้ `SharedSizeGroup` เมื่อต้องการให้หลาย Grid มีขนาด Column/Row เดียวกัน
- หลีกเลี่ยง Nested Grid มากเกินไป (ไม่เกิน 3-4 ชั้น)
- ใช้ `ColumnDefinition Width="Auto"` เฉพาะเมื่อจำเป็น

---

## ส่วนที่ 11: Wrap Up และ Outro (50:00 - 52:00)

**สรุปสิ่งที่เราได้เรียนรู้วันนี้:**

1. ✅ Grid คือ Layout Panel ที่ใช้ Row และ Column
2. ✅ RowDefinitions และ ColumnDefinitions
3. ✅ Grid.Row และ Grid.Column properties
4. ✅ การกำหนดขนาด: Auto, Fixed, Star (*)
5. ✅ Grid.RowSpan และ Grid.ColumnSpan
6. ✅ สร้าง Calculator App ด้วย Grid
7. ✅ Tips & Best Practices

**Grid เป็น Layout Panel ที่ทรงพลังที่สุดใน WPF**
- เหมาะกับ Layout ที่ซับซ้อน
- ควบคุมตำแหน่งได้แม่นยำ
- สามารถซ้อนกันได้

**ในตอนต่อไป:**

เราจะมาเรียนรู้เกี่ยวกับ **StackPanel** ซึ่งเป็น Panel ที่ใช้งานง่ายกว่า Grid
เหมาะกับ Layout แบบเส้นตรง (แนวตั้งหรือแนวนอน)

**อย่าลืม:**
- กด Like ถ้าชอบ
- Subscribe เพื่อติดตามตอนต่อไป
- Comment บอกว่าอยากให้สอนอะไรต่อไป

**ขอบคุณที่รับชมครับ แล้วพบกันใหม่ตอนหน้า สวัสดีครับ!**

---

## เอกสารอ้างอิง

### Official Documentation
- [Grid Class - Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/api/system.windows.controls.grid)
- [Panels Overview - Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/desktop/wpf/controls/panels-overview)
- [Grid Layout - WPF Tutorial](https://wpf-tutorial.com/panels/grid/)

### Properties Reference

#### Grid Properties
```
RowDefinitions: RowDefinitionCollection
ColumnDefinitions: ColumnDefinitionCollection
ShowGridLines: Boolean (for debugging)
```

#### Attached Properties
```
Grid.Row: Int32
Grid.Column: Int32
Grid.RowSpan: Int32
Grid.ColumnSpan: Int32
```

#### Size Values
```
Auto: ปรับตามเนื้อหา
Fixed (เช่น 100): ขนาดคงที่ในหน่วย pixels
Star (*): แบ่งพื้นที่ตามสัดส่วน
  * = 1*
  2* = 2 ส่วน
  3* = 3 ส่วน
```

---

## Tips & Best Practices

### 1. การใช้ Star Sizing
```xml
<!-- ดี: ใช้ * สำหรับ Responsive Layout -->
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="*"/>
    <ColumnDefinition Width="2*"/>
</Grid.ColumnDefinitions>

<!-- ไม่ดี: ใช้ Fixed Size ทำให้ไม่ Responsive -->
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="300"/>
    <ColumnDefinition Width="600"/>
</Grid.ColumnDefinitions>
```

### 2. ShowGridLines for Debugging
```xml
<!-- เปิดเพื่อดู Grid Lines ช่วงพัฒนา -->
<Grid ShowGridLines="True">
    <!-- Your content -->
</Grid>
```

### 3. Consistent Margins
```xml
<!-- ใช้ Style เพื่อความสม่ำเสมอ -->
<Grid.Resources>
    <Style TargetType="Button">
        <Setter Property="Margin" Value="2"/>
        <Setter Property="FontSize" Value="24"/>
    </Style>
</Grid.Resources>
```

### 4. MinWidth และ MinHeight
```xml
<ColumnDefinition Width="*" MinWidth="100"/>
<RowDefinition Height="Auto" MinHeight="50"/>
```

### 5. MaxWidth และ MaxHeight
```xml
<ColumnDefinition Width="*" MaxWidth="500"/>
```

---

## ตัวอย่างการใช้งานจริง

### Example 1: Login Form
```xml
<Grid Width="300" Height="200">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
        <RowDefinition Height="Auto"/>
    </Grid.RowDefinitions>
    
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    
    <TextBlock Grid.Row="0" Grid.Column="0" Text="Username:" Margin="5"/>
    <TextBox Grid.Row="0" Grid.Column="1" Margin="5"/>
    
    <TextBlock Grid.Row="1" Grid.Column="0" Text="Password:" Margin="5"/>
    <PasswordBox Grid.Row="1" Grid.Column="1" Margin="5"/>
    
    <Button Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" 
            Content="Login" Margin="5"/>
</Grid>
```

### Example 2: Dashboard Layout
```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="60"/>
        <RowDefinition Height="*"/>
        <RowDefinition Height="30"/>
    </Grid.RowDefinitions>
    
    <!-- Header -->
    <Grid Grid.Row="0" Background="Navy">
        <TextBlock Text="Dashboard" Foreground="White" 
                   VerticalAlignment="Center" Margin="10"/>
    </Grid>
    
    <!-- Content -->
    <Grid Grid.Row="1" Margin="10">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="200"/>
            <ColumnDefinition Width="*"/>
        </Grid.ColumnDefinitions>
        
        <!-- Sidebar -->
        <StackPanel Grid.Column="0" Background="LightGray">
            <Button Content="Home" Height="40"/>
            <Button Content="Reports" Height="40"/>
            <Button Content="Settings" Height="40"/>
        </StackPanel>
        
        <!-- Main Content -->
        <Grid Grid.Column="1" Margin="10,0,0,0">
            <!-- Your content here -->
        </Grid>
    </Grid>
    
    <!-- Footer -->
    <Grid Grid.Row="2" Background="DarkGray">
        <TextBlock Text="© 2025 Your Company" 
                   VerticalAlignment="Center" Margin="10"/>
    </Grid>
</Grid>
```

### Example 3: Data Grid with Tools
```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    
    <!-- Toolbar -->
    <StackPanel Grid.Row="0" Orientation="Horizontal" 
                Background="#2C3E50" Height="40">
        <Button Content="Add" Width="80" Margin="5"/>
        <Button Content="Edit" Width="80" Margin="5"/>
        <Button Content="Delete" Width="80" Margin="5"/>
    </StackPanel>
    
    <!-- Data Grid -->
    <DataGrid Grid.Row="1" Margin="10" AutoGenerateColumns="True"/>
</Grid>
```

---

## Common Mistakes (ข้อผิดพลาดที่พบบ่อย)

### ❌ ลืมกำหนด Grid.Row หรือ Grid.Column
```xml
<!-- ผิด: ไม่ระบุ Grid.Row จะไปอยู่ที่ (0,0) ทั้งหมด -->
<Button Content="Button 1"/>
<Button Content="Button 2"/>
```

### ✅ ถูกต้อง
```xml
<Button Grid.Row="0" Content="Button 1"/>
<Button Grid.Row="1" Content="Button 2"/>
```

### ❌ ใช้ Fixed Size ทำให้ไม่ Responsive
```xml
<!-- ผิด: Window resize จะเหลือพื้นที่ว่าง -->
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="300"/>
    <ColumnDefinition Width="300"/>
</Grid.ColumnDefinitions>
```

### ✅ ถูกต้อง
```xml
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="*"/>
    <ColumnDefinition Width="*"/>
</Grid.ColumnDefinitions>
```

### ❌ Nested Grid มากเกินไป
```xml
<!-- ผิด: ซับซ้อนเกินไป performance ต่ำ -->
<Grid>
    <Grid>
        <Grid>
            <Grid>
                <Button/>
            </Grid>
        </Grid>
    </Grid>
</Grid>
```

### ✅ ถูกต้อง
```xml
<!-- ใช้ Grid เดียวกับ RowSpan/ColumnSpan -->
<Grid>
    <Button Grid.RowSpan="2" Grid.ColumnSpan="2"/>
</Grid>
```

---

## Code Examples Repository

Source code สำหรับ Episode นี้สามารถดาวน์โหลดได้ที่:
- GitHub: [WPF_Episode04_Grid](https://github.com/koson/WPF_Episode04_Grid)

---

## แบบฝึกหัด

### Exercise 1: สร้าง Login Form
สร้าง Login Form ด้วย Grid ที่มี:
- Username TextBox
- Password TextBox
- Remember Me CheckBox
- Login Button

### Exercise 2: สร้าง Calculator ที่ทำงานได้
เพิ่ม Event Handler ให้ Calculator ที่เราสร้าง:
- คลิกปุ่มตัวเลขแสดงบน TextBox
- ปุ่ม C ลบค่า
- ปุ่ม = คำนวณผล

### Exercise 3: สร้าง Photo Gallery
สร้าง Grid 3x3 แสดงรูปภาพ 9 รูป
- ใช้ Image control
- เพิ่ม Border แต่ละรูป

---

**End of Script**
