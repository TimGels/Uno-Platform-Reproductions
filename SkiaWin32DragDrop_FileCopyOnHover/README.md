# Skia Win32 file copies during drag and drop

This blank Uno app has no application drag-and-drop handlers. It targets Skia
Desktop on Windows and uses Uno.Sdk 7.0.22, which resolves Uno.WinUI and
Uno.WinUI.Runtime.Win32 7.0.65.

## Reproduce

On Windows, with the .NET 10 SDK or newer installed, run from this directory:

```powershell
dotnet run --project .\Uno7DragDropRepro\Uno7DragDropRepro.csproj --framework net10.0-desktop
```

1. Drag a small, disposable local `.mkv` file from Explorer over the app window.
2. The no-drop cursor is expected: the blank page does not accept drops. Press
   Escape to cancel.
3. Check `%TEMP%\unoplatform-dragdrop` for a new copy of the file.

**Expected:** A rejected drag does not copy the file or block the application.

**Actual:** A full file copy can be created merely by hovering, even when the
drop is rejected. Large files can freeze the app and Explorer and consume
substantial temporary disk space. Use small files first and remove only copies
you identify as belonging to your test.

Related report: [TimGels/Matroska-Batch-Flow#101](https://github.com/TimGels/Matroska-Batch-Flow/issues/101).