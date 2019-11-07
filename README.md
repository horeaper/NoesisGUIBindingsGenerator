# NoesisGUIBindingsGenerator #

A simple piece of code that helps generate .g.cs files for Unity3d

## How to use ##

In NoesisPostprocessor.cs find a method called `ScanDependencies()`, in the bottom of the method body paste this code:
```
NoesisCsBindingsGenerator.GenerateCsFile(filename);
```
and you're good to go.

it will pump out code that looks like this:
```csharp
/* This file has been generated automatically. All user changes will be overwritten if the XAML is changed. */
using Noesis;

namespace Assets.UI.Views.DesignerUI
{
    [UnityEngine.HideInInspector]
    public partial class DesignerMain : UserControl
    {
        internal Grid JustNormalGrid;
        internal UniformGrid MyUniformGrid;
        
        private void InitializeComponent()
        {
            GUI.LoadComponent(this, "Assets/UI/Views/DesignerUI/DesignerMain.xaml");
            
            this.JustNormalGrid = (Grid)FindName("JustNormalGrid");
            this.MyUniformGrid = (UniformGrid)FindName("MyUniformGrid");
        }
        
        protected override bool ConnectEvent(object source, string eventName, string handlerName)
		{
			if (source is UserControl && eventName == "Loaded" && handlerName == "DesignerMain_OnLoaded") {
				((UserControl)source).Loaded += DesignerMain_OnLoaded;
				return true;
			}
            
            return false;
        }
    }
}
```
