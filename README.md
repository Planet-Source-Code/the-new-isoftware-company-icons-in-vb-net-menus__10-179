<div align="center">

## Icons in VB \.NET Menus\!\!\!\!\!


</div>

### Description

This is the first code on the .NET side of Planet Source Code's VB section to do this. I am proud to post a sample of Dr. GUI's sample code. I made a lot of changes to the original code like adding comments to it. It still needs some work. Well commented. Read the label of the screen shot, please. Don't forget to comment and vote! PS. It can be used in place of any menuitem. (Could not be uploaded. Here is the class.) ***New version bug (need help) email me if you wish to help! This is NOT C# code!
 
### More Info
 
Does not highlight. Sorta basic.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[The New iSoftware Company\!](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/the-new-isoftware-company.md)
**Level**          |Advanced
**User Rating**    |4.1 (29 globes from 7 users)
**Compatibility**  |VB\.NET
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__10-1.md)
**World**          |[\.Net \(C\#, VB\.net\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/net-c-vb-net.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/the-new-isoftware-company-icons-in-vb-net-menus__10-179/archive/master.zip)





### Source Code

```
Public Class clsMenuIcons
 'Original Code by Dr. GUI and the People at Microsoft.
 'Modifications By The New iSoftware.
 'Please give credit.
#Region " Visual Basic .NET Icons on MenuItems Class File "
 Inherits MenuItem
 Public Icon As Icon
 Public Font As Font
 Sub New(ByVal Text As String, ByVal EventHandler As EventHandler, ByVal Shortcut As Shortcut, ByVal Icon As Icon)
  MyBase.New(Text, EventHandler, Shortcut) 'Creates Base Menu Meth. and Prop.
  Me.OwnerDraw = True 'Required. Allows the OnMeasureItem and OnDrawItem overrides.
  Me.Icon = Icon 'Sets the icon.
  Me.Font = SystemInformation.MenuFont 'Sets font to normal, can be overridden.
 End Sub
 Protected Overrides Sub OnMeasureItem(ByVal E As MeasureItemEventArgs)
  MyBase.OnMeasureItem(E) 'Do this first. Fires code for this.
  Dim sfStringFormat As New StringFormat()
  sfStringFormat.HotkeyPrefix = Drawing.Text.HotkeyPrefix.Show 'The _ for &.
  sfStringFormat.SetTabStops(50, New Single() {0}) 'Declares tab.
  If Icon.Height > Font.Height Then 'Sets height.
   E.ItemHeight = Me.Icon.Height + 2 'Icon as base.
  Else
   E.ItemHeight = Me.Font.Height + 2 'Font as base.
  End If
  E.ItemWidth = CInt(E.Graphics.MeasureString(AppendShortcut(), Me.Font, 1000, sfStringFormat).Width) + Icon.Width + 5 ' Width Set
  sfStringFormat.Dispose() 'Clean Up!
 End Sub
 Protected Overrides Sub OnDrawItem(ByVal E As DrawItemEventArgs)
  MyBase.OnDrawItem(E) 'Do this first. Fires code for this.
  Dim brBrush As Brush
  Dim sfStringFormat As New StringFormat()
  E.Graphics.FillRectangle(SystemBrushes.Menu, E.Bounds) 'Draws BG.
  If Not (Icon Is Nothing) Then
   E.Graphics.DrawIcon(Icon, E.Bounds.Left + 1, E.Bounds.Top + 1) 'Draws Icon. any size works at org size.
  End If
  sfStringFormat.HotkeyPrefix = Drawing.Text.HotkeyPrefix.Show 'The _ for &.
  sfStringFormat.SetTabStops(50, New Single() {0}) 'Declares tab.
  brBrush = New SolidBrush(SystemColors.MenuText) 'Sets the brush color.
  E.Graphics.DrawString(AppendShortcut(), Me.Font, brBrush, E.Bounds.Left + Icon.Width + 10, E.Bounds.Top, sfStringFormat) 'Draws text.
  brBrush.Dispose() 'Clean Up!
  sfStringFormat.Dispose()
 End Sub
 Private Function AppendShortcut() As String 'Basicaly determines to draw the HeldButtton+AnyKey thing.
  Dim sTemp As String
  sTemp = Me.Text
  If Me.ShowShortcut And Me.Shortcut <> Shortcut.None Then
   Dim kKeys As Keys = CType(Shortcut, Keys)
   sTemp = sTemp & Convert.ToChar(9) & System.ComponentModel.TypeDescriptor.GetConverter(GetType(Keys)).ConvertToString(kKeys)
  End If
  Return sTemp
 End Function
#End Region
End Class
```

