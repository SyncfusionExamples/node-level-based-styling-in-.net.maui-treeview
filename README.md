# node-level-based-styling-in-.net.maui-treeview
This repository demonstrates how to customize the appearance of nodes based on their level in the .NET MAUI TreeView (SfTreeView) control. It provides a sample implementation using a value converter to apply different styles, such as font attributes, to nodes at various levels, enabling visually distinct and hierarchical node presentation.

## Sample

### XAML

```xaml
<ContentPage.Resources>
    <ResourceDictionary>
        <local:FontAttributesConverter x:Key="FontAttributeConverter"/>
    </ResourceDictionary>
</ContentPage.Resources>
<ContentPage.Content>
    <Grid>
        <syncfusion:SfTreeView x:Name="treeView" Grid.Row="1"
                                   AutoExpandMode="RootNodesExpanded"
                                   ChildPropertyName="SubFiles"
                                   ItemTemplateContextType="Node"                           
                                   ItemsSource="{Binding ImageNodeInfo}" >
            <syncfusion:SfTreeView.ItemTemplate>
                <DataTemplate>
                    <Grid x:Name="grid" RowSpacing="0">
                        <Grid.ColumnDefinitions>
                            ...
                        </Grid.ColumnDefinitions>
                        <Grid Grid.Column="0">
                            <Image .../>
                        </Grid>
                        <Grid Grid.Column="1">
                            <Label Text="{Binding Content.ItemName}" VerticalTextAlignment="Center" 
                                   FontAttributes="{Binding Level,Converter={x:StaticResource FontAttributeConverter}}"/>
                        </Grid>
                    </Grid>
                </DataTemplate>
            </syncfusion:SfTreeView.ItemTemplate>
        </syncfusion:SfTreeView>
    </Grid>
</ContentPage.Content>
```

### Converter

```csharp

public class FontAttributesConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        if (value == null) return null;

        var level = (int)value;
        return level == 0 ? FontAttributes.Bold : FontAttributes.Italic;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```

## Requirements to run the demo

To run the demo, refer to [System Requirements for .NET MAUI](https://help.syncfusion.com/maui/system-requirements).

Make sure that you have the compatible versions of [Visual Studio 2022](https://visualstudio.microsoft.com/downloads/ ) with the Dot NET MAUI workload and [.NET Core SDK 7.0](https://dotnet.microsoft.com/en-us/download/dotnet/7.0) or later version in your machine before starting to work on this project.

## Troubleshooting:
### Path too long exception

If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.

## License

Syncfusion® has no liability for any damage or consequence that may arise from using or viewing the samples. The samples are for demonstrative purposes. If you choose to use or access the samples, you agree to not hold Syncfusion® liable, in any form, for any damage related to use, for accessing, or viewing the samples. By accessing, viewing, or seeing the samples, you acknowledge and agree Syncfusion®'s samples will not allow you seek injunctive relief in any form for any claim related to the sample. If you do not agree to this, do not view, access, utilize, or otherwise do anything with Syncfusion®'s samples.
