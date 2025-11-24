# 🎓 Episode 04: Grid - Complete Guide

> **Problem to Solve**: How to create complex table-like layouts with precise control over rows and columns?

[![.NET](https://img.shields.io/badge/.NET-9.0-blue.svg)](https://dotnet.microsoft.com/download)
[![WPF](https://img.shields.io/badge/WPF-Layout-purple.svg)](#)
[![Episode](https://img.shields.io/badge/Episode-04-green.svg)](#)
[![Duration](https://img.shields.io/badge/Duration-52min-orange.svg)](#)

---

## 🎯 Learning Objectives

By the end of this episode, you will be able to:

- ✅ Understand when StackPanel is insufficient
- ✅ Use Grid for table-like layouts
- ✅ Master RowDefinitions and ColumnDefinitions
- ✅ Apply Auto, Fixed, and Star (*) sizing
- ✅ Use RowSpan and ColumnSpan for complex layouts
- ✅ Build real-world applications (Calculator)
- ✅ Choose between Grid and StackPanel appropriately
- ✅ Create responsive layouts with Star sizing

---

## 📖 Table of Contents

1. [The Problems We'll Solve](#the-problems-well-solve)
2. [Problem 1: StackPanel Limitations](#problem-1-stackpanel-limitations)
3. [Grid Solution](#grid-solution)
4. [RowDefinitions and ColumnDefinitions](#rowdefinitions-and-columndefinitions)
5. [Sizing Options](#sizing-options)
6. [Building a Calculator](#building-a-calculator)
7. [RowSpan and ColumnSpan](#rowspan-and-columnspan)
8. [Best Practices](#best-practices)
9. [Summary](#summary)

---

## 🤔 The Problems We'll Solve

### Today's Journey:

We'll encounter **limitations of StackPanel** and solve them with Grid:

1. **Problem 1**: StackPanel can't do side-by-side layouts easily
2. **Problem 2**: Need precise control over sizing
3. **Solution**: Grid with Rows and Columns!
4. **Real-World**: Build a Calculator app
5. **Advanced**: RowSpan and ColumnSpan

Let's start! 🚀

---

## ❌ Problem 1: StackPanel Limitations

### Scenario: Building a Login Form

You want to create a form with labels and input fields **side by side**:

```
Username: [____________]
Password: [____________]
          [Login Button]
```

### Attempt 1: Vertical StackPanel

```xml
<StackPanel>
    <TextBlock Text="Username:"/>
    <TextBox/>
    <TextBlock Text="Password:"/>
    <PasswordBox/>
    <Button Content="Login"/>
</StackPanel>
```

**Result:**
```
Username:
[__________]
Password:
[__________]
[Login]
```

**😕 Problem:** Labels and inputs are **stacked vertically**, not side by side!

### Attempt 2: Horizontal StackPanel

```xml
<StackPanel Orientation="Horizontal">
    <TextBlock Text="Username:"/>
    <TextBox Width="200"/>
    <TextBlock Text="Password:"/>
    <PasswordBox Width="200"/>
</StackPanel>
```

**Result:**
```
Username: [__________] Password: [__________]
```

**😕 Problem:** Everything is in **one row**! We wanted:
- Row 1: Username: [____]
- Row 2: Password: [____]

### Attempt 3: Nested StackPanels

```xml
<StackPanel>
    <!-- Row 1 -->
    <StackPanel Orientation="Horizontal">
        <TextBlock Text="Username:" Width="80"/>
        <TextBox Width="200"/>
    </StackPanel>
    
    <!-- Row 2 -->
    <StackPanel Orientation="Horizontal">
        <TextBlock Text="Password:" Width="80"/>
        <PasswordBox Width="200"/>
    </StackPanel>
    
    <!-- Row 3 -->
    <Button Content="Login"/>
</StackPanel>
```

**Try running this...**

✅ **It works!** But...

**😩 Problems:**
1. **Tedious to maintain** - What if we want to change label width? Change all!
2. **Not aligned properly** - Labels might have different widths
3. **No auto-sizing** - Must manually calculate widths
4. **Too much nesting** - Hard to read

**There must be a better way... 🤔**

---

## ✨ Grid Solution!

### The Better Way: Grid

**Grid is designed for table-like layouts!**

```xml
<Grid Width="300">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
    </Grid.RowDefinitions>
    
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    
    <!-- Row 0: Username -->
    <TextBlock Grid.Row="0" Grid.Column="0" Text="Username:" Margin="5"/>
    <TextBox Grid.Row="0" Grid.Column="1" Margin="5"/>
    
    <!-- Row 1: Password -->
    <TextBlock Grid.Row="1" Grid.Column="0" Text="Password:" Margin="5"/>
    <PasswordBox Grid.Row="1" Grid.Column="1" Margin="5"/>
    
    <!-- Row 2: Login Button -->
    <Button Grid.Row="2" Grid.Column="0" Grid.ColumnSpan="2" 
            Content="Login" Margin="5"/>
</Grid>
```

**Try running this...**

✅ **Perfect!** 🎉

**Notice the benefits:**
- ✅ Labels **automatically aligned** (same column)
- ✅ TextBoxes **stretch to fill** available space (Width="*")
- ✅ Easy to add/remove rows
- ✅ Clean, readable code
- ✅ Professional-looking form

---

## 🏗️ Understanding Grid Structure

### Grid Anatomy

**Grid is like a table:**

```
┌─────────────┬─────────────┬─────────────┐
│  Cell (0,0) │  Cell (0,1) │  Cell (0,2) │  ← Row 0
├─────────────┼─────────────┼─────────────┤
│  Cell (1,0) │  Cell (1,1) │  Cell (1,2) │  ← Row 1
├─────────────┼─────────────┼─────────────┤
│  Cell (2,0) │  Cell (2,1) │  Cell (2,2) │  ← Row 2
└─────────────┴─────────────┴─────────────┘
     ↑             ↑             ↑
   Col 0         Col 1         Col 2
```

**Key Concepts:**
- **Row** = Horizontal line (แถว)
- **Column** = Vertical line (คอลัมน์)
- **Cell** = Intersection of Row and Column (ช่อง)
- **Coordinates** = (Row, Column) starting from (0, 0)

### Default Grid Behavior

```xml
<Grid>
    <Button Content="Button 1"/>
    <Button Content="Button 2"/>
</Grid>
```

**What happens?**
- Grid has **1 Row, 1 Column** by default
- All elements go to **Cell (0, 0)**
- Elements **overlap** (like Grid in Episode 3)!

**Visual:**
```
┌─────────────────┐
│ Button 1        │  ← Both buttons
│ Button 2        │  ← at (0,0)!
└─────────────────┘
```

---

## 📐 RowDefinitions and ColumnDefinitions

### Defining Rows

To create multiple rows, use `<Grid.RowDefinitions>`:

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Button Grid.Row="0" Content="Row 0"/>
    <Button Grid.Row="1" Content="Row 1"/>
    <Button Grid.Row="2" Content="Row 2"/>
</Grid>
```

**Explanation:**
- `<Grid.RowDefinitions>` - Container for row definitions
- `<RowDefinition/>` - Each row (one per row)
- `Grid.Row="0"` - Attached property specifying which row

**Visual:**
```
┌────────────────┐
│    Row 0       │ ← Grid.Row="0"
├────────────────┤
│    Row 1       │ ← Grid.Row="1"
├────────────────┤
│    Row 2       │ ← Grid.Row="2"
└────────────────┘
```

### Defining Columns

To create multiple columns, use `<Grid.ColumnDefinitions>`:

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

**Visual:**
```
┌──────┬──────┬──────┐
│Col 0 │Col 1 │Col 2 │
└──────┴──────┴──────┘
   ↑      ↑      ↑
Grid.Column="0", "1", "2"
```

### Combining Rows and Columns

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

**Visual:**
```
┌─────┬─────┬─────┐
│ 0,0 │ 0,1 │ 0,2 │
├─────┼─────┼─────┤
│ 1,0 │ 1,1 │ 1,2 │
└─────┴─────┴─────┘
```

**Result:** 2×3 table (2 rows, 3 columns)!

---

## 📏 Sizing Options

### Three Ways to Size Rows and Columns:

1. **Auto** - Size to content
2. **Fixed** - Absolute size (pixels)
3. **Star (*)** - Proportional size

### 1. Auto Sizing

**Content determines size:**

```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="Auto"/>
    </Grid.ColumnDefinitions>
    
    <Button Grid.Column="0" Content="Short" Padding="10"/>
    <Button Grid.Column="1" Content="Very Long Button Text" Padding="10"/>
</Grid>
```

**Result:**
```
┌────────┬────────────────────────┐
│ Short  │ Very Long Button Text  │
└────────┴────────────────────────┘
    ↑              ↑
  Fits         Fits content
 content
```

**When to use Auto:**
- Labels that vary in length
- Content-sized panels
- Dynamic content

### 2. Fixed Sizing

**Absolute size in pixels:**

```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="100"/>
        <ColumnDefinition Width="200"/>
        <ColumnDefinition Width="150"/>
    </Grid.ColumnDefinitions>
</Grid>
```

**Result:**
```
┌──────────┬────────────────────┬──────────────┐
│  100px   │      200px         │    150px     │
└──────────┴────────────────────┴──────────────┘
```

**When to use Fixed:**
- Exact pixel dimensions needed
- Icons, images with specific sizes
- Toolbars with fixed width

**⚠️ Warning:** Not responsive! Window resize = empty space or scrolling.

### 3. Star (*) Sizing - THE MOST IMPORTANT!

**Proportional distribution of remaining space:**

#### Equal Distribution

```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
</Grid>
```

**Result:** Both columns get **50%** each

```
┌──────────────────┬──────────────────┐
│       50%        │       50%        │
└──────────────────┴──────────────────┘
```

#### Weighted Distribution

```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="2*"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
</Grid>
```

**Calculation:**
- Total parts: 2 + 1 = 3
- Column 0: 2/3 = **66.67%**
- Column 1: 1/3 = **33.33%**

**Result:**
```
┌──────────────────────────┬──────────────┐
│         66.67%           │    33.33%    │
└──────────────────────────┴──────────────┘
```

#### Mixed Sizing

```xml
<Grid Width="600">
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>    <!-- Fits content -->
        <ColumnDefinition Width="100"/>     <!-- Fixed 100px -->
        <ColumnDefinition Width="*"/>       <!-- 1 part -->
        <ColumnDefinition Width="2*"/>      <!-- 2 parts -->
    </Grid.ColumnDefinitions>
</Grid>
```

**Calculation:**
- Total width: 600px
- Auto: Let's say content = 80px
- Fixed: 100px
- Remaining: 600 - 80 - 100 = **420px**
- Star parts: 1 + 2 = 3
- Column 2 (1*): 420 × (1/3) = **140px**
- Column 3 (2*): 420 × (2/3) = **280px**

**Result:**
```
┌──────┬─────────┬──────────────┬────────────────────────┐
│ 80px │  100px  │    140px     │         280px          │
│ Auto │  Fixed  │      *       │          2*            │
└──────┴─────────┴──────────────┴────────────────────────┘
```

**When to use Star (*):**
- ✅ Responsive layouts
- ✅ Proportional sizing
- ✅ Flexible content areas
- ✅ Modern UI design

**⭐ Recommendation:** Use Star (*) as much as possible for responsive designs!

---

## 🔢 Building a Calculator

Now let's build something real - a Calculator app!

### Design Requirements

```
┌─────────────────────────┐
│           0             │ ← Display (Row 0, height 60px)
├───────┬───────┬───────┬─┤
│   7   │   8   │   9   │/│ ← Row 1
├───────┼───────┼───────┼─┤
│   4   │   5   │   6   │*│ ← Row 2
├───────┼───────┼───────┼─┤
│   1   │   2   │   3   │-│ ← Row 3
├───────┼───────┼───────┼─┤
│   C   │   0   │   =   │+│ ← Row 4
└───────┴───────┴───────┴─┘
```

### Step 1: Main Structure

```xml
<Grid Margin="20">
    <Grid.RowDefinitions>
        <RowDefinition Height="60"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
</Grid>
```

**Explanation:**
- Row 0: Fixed **60px** for display
- Row 1: **Star (*)** for buttons (takes remaining space)

### Step 2: Display Area

```xml
<TextBox Grid.Row="0" 
         Text="0" 
         FontSize="32" 
         TextAlignment="Right" 
         VerticalContentAlignment="Center" 
         Padding="10"
         IsReadOnly="True"/>
```

**Properties explained:**
- `Grid.Row="0"` - Top row
- `Text="0"` - Initial display
- `FontSize="32"` - Large digits
- `TextAlignment="Right"` - Numbers align right (like real calculators)
- `VerticalContentAlignment="Center"` - Vertically centered
- `Padding="10"` - Space inside TextBox
- `IsReadOnly="True"` - User can't type (click buttons only)

### Step 3: Button Grid

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

**Explanation:**
- `Grid.Row="1"` - Goes in bottom section
- `Margin="0,10,0,0"` - 10px space from display
- 4 Rows × 4 Columns = 16 buttons
- All use **Star (*)** = equal size buttons!

### Step 4: Row 0 Buttons (7, 8, 9, /)

```xml
<!-- Row 0: 7 8 9 / -->
<Button Grid.Row="0" Grid.Column="0" Content="7" FontSize="24" Margin="2"/>
<Button Grid.Row="0" Grid.Column="1" Content="8" FontSize="24" Margin="2"/>
<Button Grid.Row="0" Grid.Column="2" Content="9" FontSize="24" Margin="2"/>
<Button Grid.Row="0" Grid.Column="3" Content="/" FontSize="24" Margin="2" 
        Background="#FFE0A0" Foreground="#000"/>
```

**Styling:**
- `FontSize="24"` - Large numbers
- `Margin="2"` - Small gap between buttons
- `Background="#FFE0A0"` - Light orange for operators

### Step 5: Row 1 Buttons (4, 5, 6, *)

```xml
<!-- Row 1: 4 5 6 * -->
<Button Grid.Row="1" Grid.Column="0" Content="4" FontSize="24" Margin="2"/>
<Button Grid.Row="1" Grid.Column="1" Content="5" FontSize="24" Margin="2"/>
<Button Grid.Row="1" Grid.Column="2" Content="6" FontSize="24" Margin="2"/>
<Button Grid.Row="1" Grid.Column="3" Content="*" FontSize="24" Margin="2" 
        Background="#FFE0A0" Foreground="#000"/>
```

### Step 6: Row 2 Buttons (1, 2, 3, -)

```xml
<!-- Row 2: 1 2 3 - -->
<Button Grid.Row="2" Grid.Column="0" Content="1" FontSize="24" Margin="2"/>
<Button Grid.Row="2" Grid.Column="1" Content="2" FontSize="24" Margin="2"/>
<Button Grid.Row="2" Grid.Column="2" Content="3" FontSize="24" Margin="2"/>
<Button Grid.Row="2" Grid.Column="3" Content="-" FontSize="24" Margin="2" 
        Background="#FFE0A0" Foreground="#000"/>
```

### Step 7: Row 3 Buttons (C, 0, =, +)

```xml
<!-- Row 3: C 0 = + -->
<Button Grid.Row="3" Grid.Column="0" Content="C" FontSize="24" Margin="2" 
        Background="#FFA0A0" Foreground="#000"/>
<Button Grid.Row="3" Grid.Column="1" Content="0" FontSize="24" Margin="2"/>
<Button Grid.Row="3" Grid.Column="2" Content="=" FontSize="24" Margin="2" 
        Background="#A0FFA0" Foreground="#000"/>
<Button Grid.Row="3" Grid.Column="3" Content="+" FontSize="24" Margin="2" 
        Background="#FFE0A0" Foreground="#000"/>
```

**Color coding:**
- **Numbers (0-9)**: Default color (light gray)
- **Operators (+, -, *, /)**: Light orange `#FFE0A0`
- **Clear (C)**: Light red `#FFA0A0`
- **Equals (=)**: Light green `#A0FFA0`

### Complete Calculator Code

```xml
<Window x:Class="WPF_Episode04_Grid.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Calculator" Height="450" Width="400">
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
                 Padding="10"
                 IsReadOnly="True"/>
        
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
</Window>
```

**Try running this!** 🎉

You now have a professional-looking calculator interface!

---

## 🎭 RowSpan and ColumnSpan

### The Problem: Merging Cells

Sometimes you need an element to span **multiple rows** or **columns**:

```
┌─────────┬─────────┬─────────┐
│         │  Col 1  │  Col 2  │
│  Big    ├─────────┼─────────┤
│  Button │  Col 1  │  Col 2  │
│         ├─────────┼─────────┤
│         │  Col 1  │  Col 2  │
└─────────┴─────────┴─────────┘
```

### RowSpan - Span Multiple Rows

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
        <ColumnDefinition/>
    </Grid.ColumnDefinitions>
    
    <!-- Normal button -->
    <Button Grid.Row="0" Grid.Column="0" Content="Normal"/>
    
    <!-- Button spanning 3 rows -->
    <Button Grid.Row="0" Grid.Column="1" 
            Grid.RowSpan="3" 
            Content="Tall Button" 
            Background="LightBlue"/>
</Grid>
```

**Visual:**
```
┌────────┬────────────┬────────┐
│ Normal │            │        │
├────────┤   Tall     │        │
│        │   Button   │        │
├────────┤            │        │
│        │            │        │
└────────┴────────────┴────────┘
```

**Explanation:**
- `Grid.RowSpan="3"` - Spans from Row 0 to Row 2 (3 rows total)
- Button occupies cells (0,1), (1,1), and (2,1)

### ColumnSpan - Span Multiple Columns

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
    
    <!-- Button spanning 3 columns -->
    <Button Grid.Row="0" Grid.Column="0" 
            Grid.ColumnSpan="3" 
            Content="Wide Button" 
            Background="LightGreen"/>
    
    <Button Grid.Row="1" Grid.Column="0" Content="Col 0"/>
    <Button Grid.Row="1" Grid.Column="1" Content="Col 1"/>
    <Button Grid.Row="1" Grid.Column="2" Content="Col 2"/>
</Grid>
```

**Visual:**
```
┌─────────────────────────────────┐
│         Wide Button             │
├──────────┬──────────┬───────────┤
│  Col 0   │  Col 1   │   Col 2   │
└──────────┴──────────┴───────────┘
```

### Both RowSpan and ColumnSpan

```xml
<Button Grid.Row="1" Grid.Column="1" 
        Grid.RowSpan="2" 
        Grid.ColumnSpan="2" 
        Content="Big Button" 
        Background="Yellow"/>
```

**Visual:**
```
┌──────┬──────┬──────┬──────┐
│      │      │      │      │
├──────┼──────────────┼──────┤
│      │              │      │
│      │  Big Button  │      │
├──────┤              ├──────┤
│      │              │      │
└──────┴──────────────┴──────┘
```

**Spans:**
- 2 Rows (Row 1 and Row 2)
- 2 Columns (Column 1 and Column 2)

### Real-World Example: Dashboard Layout

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="60"/>
        <RowDefinition Height="*"/>
        <RowDefinition Height="30"/>
    </Grid.RowDefinitions>
    
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="200"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    
    <!-- Header spans both columns -->
    <Grid Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2" 
          Background="#2C3E50">
        <TextBlock Text="Dashboard" 
                   Foreground="White" 
                   VerticalAlignment="Center" 
                   Margin="10"/>
    </Grid>
    
    <!-- Sidebar (left column, middle row) -->
    <StackPanel Grid.Row="1" Grid.Column="0" Background="#34495E">
        <Button Content="Home" Height="40"/>
        <Button Content="Reports" Height="40"/>
        <Button Content="Settings" Height="40"/>
    </StackPanel>
    
    <!-- Main content (right column, middle row) -->
    <Border Grid.Row="1" Grid.Column="1" 
            Background="White" 
            Margin="10">
        <TextBlock Text="Main Content Area" Margin="10"/>
    </Border>
    
    <!-- Footer spans both columns -->
    <Grid Grid.Row="2" Grid.Column="0" Grid.ColumnSpan="2" 
          Background="#95A5A6">
        <TextBlock Text="© 2025 Your Company" 
                   VerticalAlignment="Center" 
                   Margin="10"/>
    </Grid>
</Grid>
```

**Visual:**
```
┌────────────────────────────────────┐
│          Dashboard (Header)        │ ← ColumnSpan=2
├───────────┬────────────────────────┤
│  Sidebar  │                        │
│  - Home   │   Main Content Area    │
│  - Report │                        │
│  - Setting│                        │
├───────────┴────────────────────────┤
│      © 2025 Your Company (Footer)  │ ← ColumnSpan=2
└────────────────────────────────────┘
```

---

## ⚠️ Common Problems & Solutions

### Problem 1: Elements Overlap

```xml
<!-- ❌ Problem: Both buttons go to Row 0 (default) -->
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Button Content="Button 1"/>  <!-- Row 0 by default -->
    <Button Content="Button 2"/>  <!-- Row 0 by default - OVERLAP! -->
</Grid>
```

**Solution:** Always specify `Grid.Row` and `Grid.Column`

```xml
<!-- ✅ Solution -->
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Button Grid.Row="0" Content="Button 1"/>
    <Button Grid.Row="1" Content="Button 2"/>
</Grid>
```

### Problem 2: Not Responsive

```xml
<!-- ❌ Problem: Fixed sizes, lots of empty space when window resizes -->
<Grid Width="800">
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="300"/>
        <ColumnDefinition Width="300"/>
    </Grid.ColumnDefinitions>
</Grid>
```

**Solution:** Use Star (*) sizing

```xml
<!-- ✅ Solution -->
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
</Grid>
```

### Problem 3: Content Cut Off

```xml
<!-- ❌ Problem: Fixed height too small, content hidden -->
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="50"/>  <!-- Too small! -->
    </Grid.RowDefinitions>
    
    <TextBlock Text="Very long text that will be cut off..." 
               TextWrapping="Wrap"/>
</Grid>
```

**Solution 1:** Use `Auto` sizing

```xml
<!-- ✅ Solution 1: Auto height -->
<Grid.RowDefinitions>
    <RowDefinition Height="Auto"/>  <!-- Fits content -->
</Grid.RowDefinitions>
```

**Solution 2:** Use `ScrollViewer`

```xml
<!-- ✅ Solution 2: Scrollable -->
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    
    <ScrollViewer>
        <TextBlock Text="Very long text..." TextWrapping="Wrap"/>
    </ScrollViewer>
</Grid>
```

---

## ✅ Best Practices

### Do's ✅

1. **Always specify Grid.Row and Grid.Column**
   ```xml
   <!-- Even if it's Row 0, Column 0 - be explicit! -->
   <Button Grid.Row="0" Grid.Column="0" Content="Button"/>
   ```

2. **Use Star (*) for responsive layouts**
   ```xml
   <ColumnDefinition Width="*"/>  <!-- Flexible -->
   ```

3. **Use Auto for content-sized elements**
   ```xml
   <ColumnDefinition Width="Auto"/>  <!-- Labels, etc. -->
   ```

4. **Use ShowGridLines for debugging**
   ```xml
   <Grid ShowGridLines="True">
       <!-- See the grid structure! -->
   </Grid>
   ```

5. **Combine with other panels**
   ```xml
   <Grid>
       <StackPanel Grid.Row="0" Grid.Column="1">
           <!-- StackPanel inside Grid cell -->
       </StackPanel>
   </Grid>
   ```

### Don'ts ❌

1. **Don't use too many nested Grids**
   ```xml
   <!-- ❌ Avoid deep nesting (max 3-4 levels) -->
   <Grid>
       <Grid>
           <Grid>
               <Grid>  <!-- Too deep! -->
   ```

2. **Don't use all Fixed sizes**
   ```xml
   <!-- ❌ Not responsive -->
   <ColumnDefinition Width="300"/>
   <ColumnDefinition Width="400"/>
   ```

3. **Don't forget Row/Column definitions**
   ```xml
   <!-- ❌ Forgot to define rows = overlap! -->
   <Grid>
       <Button Grid.Row="0" Content="Button 1"/>
       <Button Grid.Row="1" Content="Button 2"/>  <!-- No Row 1 defined! -->
   </Grid>
   ```

4. **Don't overuse RowSpan/ColumnSpan**
   ```xml
   <!-- ❌ Makes layout hard to understand -->
   ```

---

## 📊 Grid vs StackPanel

### Use StackPanel When:

✅ **Simple linear stacking**
```xml
<StackPanel>
    <Button Content="Button 1"/>
    <Button Content="Button 2"/>
    <Button Content="Button 3"/>
</StackPanel>
```

✅ **Vertical menus**  
✅ **Horizontal toolbars**  
✅ **No side-by-side layout needed**

### Use Grid When:

✅ **Side-by-side layouts**
```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    <TextBlock Grid.Column="0" Text="Label:"/>
    <TextBox Grid.Column="1"/>
</Grid>
```

✅ **Forms** (labels + inputs)  
✅ **Dashboards** (header, sidebar, main, footer)  
✅ **Table-like layouts**  
✅ **Complex responsive designs**

---

## 🎓 Summary

### What We Learned:

1. **Problem: StackPanel limitations**
   - Can't do side-by-side easily
   - Need nested StackPanels (tedious)

2. **Solution: Grid**
   - Table-like layout
   - Rows and Columns
   - Precise control

3. **RowDefinitions and ColumnDefinitions**
   - Define grid structure
   - Grid.Row and Grid.Column to position

4. **Sizing Options**
   - **Auto**: Fits content
   - **Fixed**: Absolute pixels
   - **Star (*)**: Proportional (responsive!)

5. **Built Calculator app**
   - Real-world example
   - Nested Grids
   - Color-coded buttons

6. **RowSpan and ColumnSpan**
   - Merge cells
   - Complex layouts

### Key Takeaways:

✅ **Grid = Most powerful layout panel** in WPF  
✅ **Use Star (*) for responsive** layouts  
✅ **Always specify Grid.Row/Column** to avoid overlap  
✅ **Combine with other panels** for best results  
✅ **Perfect for forms, dashboards, tables**  
✅ **ShowGridLines="True"** for debugging  
⚠️ **Don't nest too deep** (max 3-4 levels)  
⚠️ **StackPanel for simple lists**, Grid for complex layouts

### When to Use:

- ✅ **Grid**: Forms, dashboards, complex layouts
- ✅ **StackPanel**: Menus, toolbars, simple lists
- ✅ **Nested Grid + StackPanel**: Best of both worlds!

---

## 🔗 Related Topics

- **Previous**: [Episode 03 - StackPanel](../WPF_Episode03_StackPanel) - Simple linear layouts
- **Next**: [Episode 05 - WrapPanel](../WPF_Episode05_WrapPanel) - Responsive wrapping
- **Complement**: [Episode 09 - ScrollViewer](../WPF_Episode09_ScrollView) - Scrollable content
- **Advanced**: [Episode 14 - TabControl](../WPF_Episode14_TabControl) - Multi-page layouts

---

## 📚 Additional Resources

- [Tutorial Script](Script/YouTube-Script.md) - Full 52-minute script with calculator demo
- [Quick Reference](notes.md) - Cheat sheet for quick lookup
- [Official Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.windows.controls.grid)

---

## ⏭️ Next Episode

**Episode 05: WrapPanel - Responsive Wrapping**
- Understanding WrapPanel behavior
- Horizontal and Vertical wrapping
- Responsive designs
- Building tag clouds and photo galleries

---

**Made with ❤️ for WPF learners**

*Last Updated: November 24, 2025*
