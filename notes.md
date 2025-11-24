# Episode 04: Grid - Quick Reference

> 💡 **Core Concept**: Powerful table-like layout with Rows and Columns - solve the "need precise control" problem!

---

## 🎯 The Problem Grid Solves

**Problem 1: StackPanel limitations**
```xml
<!-- ❌ StackPanel can't do side-by-side layouts easily -->
<StackPanel>
    <TextBlock Text="Name:"/>
    <TextBox/>  <!-- Always below, not beside! -->
</StackPanel>
```

**Problem 2: Need precise positioning**
```xml
<!-- ❌ Canvas requires absolute positioning (x, y) -->
<Canvas>
    <Button Canvas.Left="50" Canvas.Top="100"/>  <!-- Hard to maintain! -->
</Canvas>
```

**Solution: Grid!**
```xml
<!-- ✅ Easy table-like layout! -->
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    
    <TextBlock Grid.Row="0" Grid.Column="0" Text="Name:"/>
    <TextBox Grid.Row="0" Grid.Column="1"/>
    
    <TextBlock Grid.Row="1" Grid.Column="0" Text="Email:"/>
    <TextBox Grid.Row="1" Grid.Column="1"/>
</Grid>
```

---

## 📋 Basic Syntax

### Simple Grid (1 Row, 1 Column - Default)
```xml
<Grid>
    <Button Content="Click Me"/>
    <!-- Fills entire Grid -->
</Grid>
```

### Multiple Rows
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

### Multiple Columns
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

### Rows AND Columns (Table Layout)
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

---

## 🔧 Sizing Options

### 1. Auto - Size to Content
```xml
<ColumnDefinition Width="Auto"/>
<RowDefinition Height="Auto"/>
<!-- Shrinks/expands to fit content -->
```

### 2. Fixed - Absolute Size (Pixels)
```xml
<ColumnDefinition Width="100"/>
<RowDefinition Height="60"/>
<!-- Always 100px or 60px -->
```

### 3. Star (*) - Proportional Size
```xml
<!-- Equal distribution -->
<ColumnDefinition Width="*"/>
<ColumnDefinition Width="*"/>
<!-- Both get 50% -->

<!-- Weighted distribution -->
<ColumnDefinition Width="2*"/>
<ColumnDefinition Width="*"/>
<!-- First gets 66.67%, second gets 33.33% -->

<!-- Mixed sizes -->
<ColumnDefinition Width="Auto"/>     <!-- Fits content -->
<ColumnDefinition Width="100"/>      <!-- Fixed 100px -->
<ColumnDefinition Width="*"/>        <!-- Takes remaining space -->
```

---

## 📐 Spanning Cells

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
    </Grid.ColumnDefinitions>
    
    <Button Grid.Row="0" Grid.Column="0" Content="Normal"/>
    <Button Grid.Row="0" Grid.Column="1" 
            Grid.RowSpan="3" 
            Content="Spans 3 Rows" 
            Background="LightBlue"/>
    <!-- Spans from Row 0 to Row 2 -->
</Grid>
```

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
    
    <Button Grid.Row="0" Grid.Column="0" 
            Grid.ColumnSpan="3" 
            Content="Spans 3 Columns" 
            Background="LightGreen"/>
    <!-- Spans from Column 0 to Column 2 -->
</Grid>
```

### Both RowSpan and ColumnSpan
```xml
<Button Grid.Row="1" Grid.Column="1" 
        Grid.RowSpan="2" 
        Grid.ColumnSpan="2" 
        Content="2x2 Big Button" 
        Background="Yellow"/>
```

---

## 💡 Common Patterns

### Pattern 1: Login Form
```xml
<Grid Width="300" Margin="20">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    
    <!-- Username -->
    <TextBlock Grid.Row="0" Grid.Column="0" Text="Username:" Margin="5"/>
    <TextBox Grid.Row="0" Grid.Column="1" Margin="5"/>
    
    <!-- Password -->
    <TextBlock Grid.Row="1" Grid.Column="0" Text="Password:" Margin="5"/>
    <PasswordBox Grid.Row="1" Grid.Column="1" Margin="5"/>
    
    <!-- Login Button -->
    <Button Grid.Row="2" Grid.Column="0" Grid.ColumnSpan="2" 
            Content="Login" Margin="5"/>
</Grid>
```

### Pattern 2: Calculator Layout
```xml
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
             VerticalContentAlignment="Center"/>
    
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
        <Button Grid.Row="0" Grid.Column="3" Content="/" FontSize="24" Margin="2"/>
        
        <!-- More buttons... -->
    </Grid>
</Grid>
```

### Pattern 3: Dashboard Layout
```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="60"/>     <!-- Header -->
        <RowDefinition Height="*"/>      <!-- Content -->
        <RowDefinition Height="30"/>     <!-- Footer -->
    </Grid.RowDefinitions>
    
    <!-- Header -->
    <Grid Grid.Row="0" Background="#2C3E50">
        <TextBlock Text="Dashboard" 
                   Foreground="White" 
                   VerticalAlignment="Center" 
                   Margin="10"/>
    </Grid>
    
    <!-- Content -->
    <Grid Grid.Row="1">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="200"/>  <!-- Sidebar -->
            <ColumnDefinition Width="*"/>    <!-- Main -->
        </Grid.ColumnDefinitions>
        
        <!-- Sidebar -->
        <StackPanel Grid.Column="0" Background="#34495E">
            <Button Content="Home" Height="40"/>
            <Button Content="Reports" Height="40"/>
        </StackPanel>
        
        <!-- Main Content -->
        <Border Grid.Column="1" Background="White" Margin="10">
            <TextBlock Text="Main Content Area"/>
        </Border>
    </Grid>
    
    <!-- Footer -->
    <Grid Grid.Row="2" Background="#95A5A6">
        <TextBlock Text="© 2025 Company" Margin="10"/>
    </Grid>
</Grid>
```

---

## ⚠️ Common Problems & Solutions

### Problem 1: Elements Overlap
```xml
<!-- ❌ Problem: No Grid.Row specified, all go to Row 0! -->
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Button Content="Button 1"/>  <!-- Row 0 (default) -->
    <Button Content="Button 2"/>  <!-- Row 0 (default) - OVERLAPS! -->
</Grid>

<!-- ✅ Solution: Specify Grid.Row -->
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Button Grid.Row="0" Content="Button 1"/>
    <Button Grid.Row="1" Content="Button 2"/>
</Grid>
```

### Problem 2: Fixed Size Not Responsive
```xml
<!-- ❌ Problem: Fixed sizes, window resize = empty space -->
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="300"/>
    <ColumnDefinition Width="300"/>
</Grid.ColumnDefinitions>

<!-- ✅ Solution: Use Star (*) for responsive -->
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="*"/>
    <ColumnDefinition Width="*"/>
</Grid.ColumnDefinitions>
```

### Problem 3: Content Cut Off
```xml
<!-- ❌ Problem: Fixed row height, content overflows -->
<Grid.RowDefinitions>
    <RowDefinition Height="50"/>  <!-- Too small! -->
</Grid.RowDefinitions>

<!-- ✅ Solution 1: Use Auto -->
<Grid.RowDefinitions>
    <RowDefinition Height="Auto"/>  <!-- Fits content -->
</Grid.RowDefinitions>

<!-- ✅ Solution 2: Use ScrollViewer -->
<Grid.RowDefinitions>
    <RowDefinition Height="*"/>
</Grid.RowDefinitions>
<ScrollViewer Grid.Row="0">
    <!-- Content can scroll -->
</ScrollViewer>
```

---

## 🎨 StackPanel vs Grid

### Use StackPanel When:
```xml
<!-- ✅ Simple linear stacking -->
<StackPanel>
    <Button Content="Button 1"/>
    <Button Content="Button 2"/>
    <Button Content="Button 3"/>
</StackPanel>
```

### Use Grid When:
```xml
<!-- ✅ Side-by-side layout -->
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    
    <TextBlock Grid.Column="0" Text="Label:"/>
    <TextBox Grid.Column="1"/>
</Grid>

<!-- ✅ Table-like layout -->
<Grid>
    <!-- 3x3 table -->
</Grid>

<!-- ✅ Complex responsive layouts -->
<Grid>
    <!-- Header, Sidebar, Main, Footer -->
</Grid>
```

---

## ✅ Best Practices

### Do's ✅
- **Always specify Grid.Row and Grid.Column** (even if 0)
- **Use Star (*) for responsive layouts**
- **Use Auto for content-sized elements**
- **Use ShowGridLines="True" for debugging**
- **Combine with other panels** (StackPanel inside Grid cell)

### Don'ts ❌
- **Don't use too many nested Grids** (max 3-4 levels)
- **Don't use all Fixed sizes** (not responsive)
- **Don't forget Row/Column definitions** (overlap!)
- **Don't overuse RowSpan/ColumnSpan** (hard to maintain)

---

## 🔍 Debugging Tips

### Show Grid Lines
```xml
<Grid ShowGridLines="True">
    <!-- Visualize the grid structure! -->
</Grid>
```

### Color Backgrounds
```xml
<Grid>
    <Border Grid.Row="0" Background="Red" Opacity="0.3"/>
    <Border Grid.Row="1" Background="Blue" Opacity="0.3"/>
    <!-- See actual cell boundaries -->
</Grid>
```

---

## 💻 Code Behind Tips

### Adding to Grid Dynamically
```csharp
// Create button
Button btn = new Button
{
    Content = "Dynamic Button",
    Margin = new Thickness(5)
};

// Set Grid position
Grid.SetRow(btn, 1);
Grid.SetColumn(btn, 2);

// Add to Grid
MyGrid.Children.Add(btn);

// Spanning
Grid.SetRowSpan(btn, 2);
Grid.SetColumnSpan(btn, 3);
```

### Getting Grid Position
```csharp
int row = Grid.GetRow(myButton);
int col = Grid.GetColumn(myButton);
int rowSpan = Grid.GetRowSpan(myButton);
int colSpan = Grid.GetColumnSpan(myButton);
```

---

## 📊 Quick Comparison

| Feature | Grid | StackPanel | Canvas |
|---------|------|------------|--------|
| **Layout Type** | Table | Linear | Absolute |
| **Setup Complexity** | Medium | Easy | Hard |
| **Flexibility** | High | Low | Medium |
| **Responsive** | Yes (with *) | Yes | No |
| **Overlapping** | Yes | No | Yes |
| **Best For** | Forms, Dashboards | Menus, Lists | Custom layouts |

---

## 🎯 When to Use Grid

### ✅ Perfect For:
- **Forms** (labels + inputs side by side)
- **Dashboards** (header, sidebar, main, footer)
- **Calculator layouts** (button grids)
- **Data entry screens** (multiple fields)
- **Complex responsive layouts**

### ❌ Don't Use For:
- **Simple vertical lists** (use StackPanel)
- **Wrapping items** (use WrapPanel)
- **Free positioning** (use Canvas)
- **Document flow** (use FlowDocument)

---

## 🔄 Nested Grid Example

### Combining Multiple Grids
```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    
    <!-- Outer Grid: Header and Content -->
    
    <!-- Header Grid -->
    <Grid Grid.Row="0" Background="#2C3E50" Height="60">
        <StackPanel Orientation="Horizontal" VerticalAlignment="Center">
            <TextBlock Text="My App" Foreground="White" Margin="10"/>
        </StackPanel>
    </Grid>
    
    <!-- Content Grid -->
    <Grid Grid.Row="1">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="200"/>
            <ColumnDefinition Width="*"/>
        </Grid.ColumnDefinitions>
        
        <!-- Sidebar Grid -->
        <Grid Grid.Column="0" Background="#34495E">
            <StackPanel>
                <Button Content="Item 1" Height="40"/>
                <Button Content="Item 2" Height="40"/>
            </StackPanel>
        </Grid>
        
        <!-- Main Content Grid -->
        <Grid Grid.Column="1" Margin="10">
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
            
            <!-- Toolbar -->
            <StackPanel Grid.Row="0" Orientation="Horizontal">
                <Button Content="New" Margin="5"/>
                <Button Content="Save" Margin="5"/>
            </StackPanel>
            
            <!-- Content Area -->
            <Border Grid.Row="1" BorderBrush="Gray" BorderThickness="1" Margin="0,10,0,0">
                <TextBlock Text="Main content area"/>
            </Border>
        </Grid>
    </Grid>
</Grid>
```

---

## 📝 Key Takeaways

✅ **Grid** = Table-like layout with Rows and Columns  
✅ **RowDefinitions/ColumnDefinitions** = Define structure  
✅ **Grid.Row/Grid.Column** = Position elements  
✅ **Auto** = Fits content  
✅ **Fixed** = Absolute size (pixels)  
✅ **Star (*)** = Proportional size (responsive)  
✅ **RowSpan/ColumnSpan** = Merge cells  
✅ **Most powerful panel** in WPF  
⚠️ **Always specify Row/Column** to avoid overlap  
⚠️ **Use Star (*) for responsive** layouts  

---

## 🔗 Related Topics

- **Previous**: Episode 03 - StackPanel (simple linear layouts)
- **Next**: Episode 05 - WrapPanel (responsive wrapping)
- **Complement**: Episode 09 - ScrollViewer (scrollable content)
- **Advanced**: Episode 14 - TabControl (multi-page layouts)

---

## 📚 Resources

- [Full Script](Script/YouTube-Script.md) - Complete tutorial with calculator demo
- [Complete Guide](README.md) - Detailed documentation
- [Official Docs](https://docs.microsoft.com/en-us/dotnet/api/system.windows.controls.grid)

---

**Quick Reference Version 1.0** | Last Updated: November 24, 2025
