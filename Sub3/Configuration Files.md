# Configuration files

- [Kiosk Server](#kiosk-server)
- [Sample Application](#sample-application)

## Kiosk Server

Configuration files for the server are located in the installation folder:
 ```Program Files (x86)\Wacom Ink SDK for Multi-Display```

The principal folders are listed and detailed below:
- [Config](#server-config) - server app configuration options

Resources folder:

- [DefinitionResources](#server-definitionresources) - icon images used in the kiosk display
- [Keyboards](#server-keyboards) - virtual keyboard layouts
- [Media](#server-media) - images and videos for the Idle mode slideshow
- [Mirroring](#server-mirroring) - icon images for the mirror feature

  
### Server Config

#### app_config.json
A sample configuration is shown below with application notes // 
```
{
  "ServerEndpoint": "localhost",
  "HasStepping": true,
  "HasThumbnail": true,
  "TcpPort": 5555,
  "ZoomingFactor": 2,
  "ControlBorderBrush": "#FF000000",
  "ControlBorderThickness": 1,
  "ClientCertificate": "MyClient.pfx",
  "ClientCertificatePassword": "password", 
  "DefaultDocumentFileName": "DocumentViewLeftPanel.xaml",
  "MirroringConfig": {
    "OperatorWindowWidth": 1024,
    "LeftClickAction": "ShowImage",
    "RightClickAction": "ExecuteAction",
    "IndicatorPngWidth": 100,
    "IndicatorHorizontalAlignment": "Center"
  },
  "IdleConfig": {
    "MediaType": "videos",              // videos or images
    "DefaultOrCustomGroup": "default",  // custom uses the custom media resources
    "SlideShowInterval": 1, 
    "RemoteMediaDir": ""
  },
  "DocumentViewConfig": {
    "ButtonsConfiguration": [
      {
        "Name": "PageSteppingBtn",
        "ButtonAction": "InputStepping"
      },
      {
        "Name": "ThumbnailsBtn",
        "ButtonAction": "ToggleThumbnails"
      },
      {
        "Name": "ZoomBtn",
        "ButtonAction": "ToggleZoom",
        "ToggleImageOnPath": "/zoomin.png",
        "ToggleImageOffPath": "/zoomout.png"
      },
      {
        "Name": "ScrollToTop",
        "ButtonAction": "ScrollToTop"
      }
    ]
  },
  "SignatureViewConfig": {
    "ButtonsConfiguration": [
      {
        "Name": "ClearSignature",
        "ButtonAction": "ClearSignature"
      },
      {
        "Name": "AcceptSignature",
        "ButtonAction": "AcceptSignature"
      },
      {
        "Name": "CancelSignature",
        "ButtonAction": "CancelSignature"
      }
    ]
  }
}
```

#### log_config.json

Log files are supported using the SiriLog library.
A sample configuration is shown below with application notes // 
```
{
  "Serilog": {
    "Using": [
      "Serilog.Sinks.Console",
      "Serilog.Sinks.File"
    ],
    "MinimumLevel": "Information",
    "WriteTo": [
      {
        "Name": "Console",
        "Args": { "outputTemplate": "[{Timestamp:HH:mm:ss:ms} {Level:u3}] {Message:lj}{NewLine}{Exception}" }
      },
      {
        "Name": "Debug",
        "Args": { "outputTemplate": "[{Timestamp:HH:mm:ss:ms} {Level:u3}] {Message:lj}{NewLine}{Exception}" }
      },
      {
        "Name": "File",
        "Args": {
          "path": "%localappdata%\\Wacom\\MultiMonitor\\Logs\\kiosk_sdk_.log",
          "outputTemplate": "[{Timestamp:HH:mm:ss} {Level:u3}] {Message:lj}{NewLine}{Exception}",
          "rollingInterval": "Day"
        }
      }
    ],
    "Enrich": [ "FromLogContext", "WithMachineName", "WithThreadId" ],
    "Properties": {
      "Application": "Wacom.Kiosk.App"
    }
  }
}
```

### Server DefinitionResources
 - icon images used in the kiosk display
### Server Keyboards
 - virtual keyboard layouts
### Server Media
Images and videos for the Idle mode slideshow are saved in subfolders:
- images
    - default
    - custom - user supplied images in subfolders
- videos
    - default
    - custom - user supplied videos in subfolders

## Server Mirroring 
- icon images for mirror feature

---

## Sample Application 

The principal folders are listed and detailed below:

- [Config](#sample-code-config) - sample app configuration options

Resources folder:
Configuration and demonstration files for the control application are located in the Resources folder:
 ```Sample Code\Resources```

- [Definitions](#sample-code-definitions) - xaml configuration files 
- [Documents](#sample-code-documents) - sample pdf and html documents
- [Keyboards](#sample-code-keyboards) - virtual keyboard definitions
- [media](#sample-code-media) - images and video for the Idle mode slideshow

### Sample Code Config

#### app_config.json
A sample configuration is shown below with application notes // 
```
{
  "ClientName": "Tablet Client",
  "ServerEndpoint": "localhost",
  "HasStepping": true,
  "HasThumbnail": true,
  "TcpPort": 5555,
  "ZoomingFactor": 2,
  "ControlBorderBrush": "#FF000000",
  "ControlBorderThickness": 1,
  "MirroringConfig": {
    "OperatorWindowWidth": 1024,
    "LeftClickAction": "ShowImage",
    "RightClickAction": "ExecuteAction",
    "IndicatorPngWidth": 100,
    "IndicatorHorizontalAlignment": "Center"
  },
  "IdleConfig": {
    "MediaType": "videos",
    "DefaultOrCustomGroup": "test",
    "SlideShowInterval": 1,
    "RemoteMediaDir": ""
  },
  "DocumentViewConfig": {
    "ButtonsConfiguration": [
      {
        "Name": "PageSteppingBtn",
        "ButtonAction": "InputStepping"
      },
      {
        "Name": "ThumbnailsBtn",
        "ButtonAction": "ToggleThumbnails"
      },
      {
        "Name": "ZoomBtn",
        "ButtonAction": "ToggleZoom",
        "ToggleImageOnPath": "/zoomin.png",
        "ToggleImageOffPath": "/zoomout.png"
      },
      {
        "Name": "ScrollToTop",
        "ButtonAction": "ScrollToTop"
      }
    ]
  },
  "SignatureViewConfig": {
    "ButtonsConfiguration": [
      {
        "Name": "ClearSignature",
        "ButtonAction": "ClearSignature"
      },
      {
        "Name": "AcceptSignature",
        "ButtonAction": "AcceptSignature"
      },
      {
        "Name": "CancelSignature",
        "ButtonAction": "CancelSignature"
      }
    ]
  }
}
```

#### signature_config.json

Signature capture behaviour is defined by the configuration file.
A sample configuration is shown below with application notes // 
```
{
    "X": 0,
    "Y": 0,
    "Width": 1920,
    "Height": 1080,
    "AreaPercent": 0.5,                 // specifies the size of the capture window
    "PenTrackingType": "Unlimited",     // 'Limited' restricts pen input to the capture window
    "SignatureViewType": "External",
    "SignatureFormat": "Fss"
}
```

### Sample Code Definitions
The UI xaml configuration files define the kiosk display area for certain operations in the sample app, for example *Open Document*.
One such example follows with application notes //
In general:
- width and height dimensions are specified but automatically scaled by the server to handle different size displays
- object names are preset to match the application code, as discussed below.
- callback functions (Click="callback") are omitted as discussed below

This example defines a kiosk display layout with buttons in the left column, a document display area, and buttons in the right hand column:
```
<Window
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:Wacom.Kiosk.App"
        mc:Ignorable="d"
        x:Name="DocumentView"
        Title="DocumentView" WindowStyle="None" Width="1920" Height="1080">  // the dimensions are scaled automatically by the server to account for different size displays

    <Grid>
        <Grid Panel.ZIndex="2" HorizontalAlignment="Left" Width="150" Background="Transparent">
            <StackPanel Panel.ZIndex="2" Orientation="Vertical" >
                <!--START Page back button-->
                <Button x:Name="PageBack" Width="100" Height="100" BorderThickness="0" HorizontalAlignment="Left" Margin="25,0,25,0" VerticalAlignment="Top">
                    <Button.Background>
                        <ImageBrush ImageSource="backwards.png"/>
                    </Button.Background>
                </Button>
                <!--END Page back button-->
                <!--START Open Mirroring button-->
                <Button x:Name="OpenMirroring" Width="100" Height="100" BorderThickness="0" Margin="25,0,25,0">
                    <Button.Background>
                        <ImageBrush ImageSource="openmirroring.png"/>
                    </Button.Background>
                </Button>
                <!--END Open Mirroring button-->
                <!--START Close Mirroring button-->
                <Button x:Name="CloseMirroring" Width="100" Height="100" BorderThickness="0" Margin="25,0,25,0">
                    <Button.Background>
                        <ImageBrush ImageSource="closemirroring.png"/>
                    </Button.Background>
                </Button>
                <!--END Close Mirroring button-->

                <!--START Document accepted button-->
                <Button x:Name="DocumentAccepted" BorderThickness="0" Width="100" Height="100" Margin="25,0,25,0" VerticalAlignment="Top" HorizontalAlignment="Left" >
                    <Button.Background>
                        <ImageBrush ImageSource="check.png"/>
                    </Button.Background>
                </Button>
                <!--END Document accepted button-->
                <!--START Document rejected button-->
                <Button x:Name="DocumentRejected" BorderThickness="0" Width="100" Height="100" Margin="25,0,25,0" VerticalAlignment="Top" HorizontalAlignment="Left" >
                    <Button.Background>
                        <ImageBrush ImageSource="close.png"/>
                    </Button.Background>
                </Button>
                <!--END Document rejected button-->
            </StackPanel>
        </Grid>
        <Grid Panel.ZIndex="1" x:Name="WacomKioskDocumentImageContainer" Width="1920" >
        </Grid>
        <Grid Panel.ZIndex="2" HorizontalAlignment="Right" Width="150" Background="Transparent">
            <StackPanel Panel.ZIndex="2" Orientation="Vertical">
                <!--START Page next button-->
                <Button x:Name="PageNext" Width="100" Height="100" BorderThickness="0" HorizontalAlignment="Right" Margin="25,0,25,0" VerticalAlignment="Top">
                    <Button.Background>
                        <ImageBrush ImageSource="forwards.png"/>
                    </Button.Background>
                </Button>
                <!--END Page next button-->
                <!--START Zoom button-->
                <Button x:Name="ZoomBtn" Width="100" Height="100" BorderThickness="0" Margin="25,0,25,0" VerticalAlignment="Top" HorizontalAlignment="Left" >
                    <Button.Background>
                        <ImageBrush ImageSource="zoomin.png"/>
                    </Button.Background>
                </Button>
                <!--END Zoom button-->
                <!--START Page stepping button-->
                <Button x:Name="PageSteppingBtn" Width="100" Height="100" BorderThickness="0" Margin="25,0,25,0">
                    <Button.Background>
                        <ImageBrush ImageSource="stepping.png"/>
                    </Button.Background>
                </Button>
                <!--END Page stepping button-->
                <!--START Thumbnails button-->
                <Button x:Name="ThumbnailsBtn" Width="100" Height="100" BorderThickness="0" Margin="25,0,25,0">
                    <Button.Background>
                        <ImageBrush ImageSource="thumbs.png"/>
                    </Button.Background>
                </Button>
                <!--END Thumbnails button-->
            </StackPanel>
        </Grid>
    </Grid>

</Window>
```
The xaml contents can be created using the Visual Studio XAML Designer but note that the controls exclude the autogenerated Click function names.
This is because the application code contains message handlers for expected UI click events for pre-named controls.
For example when the button named 'PageBack' is clicked the message received by the application is identified as such. In this example see MainWindow.xamls.cs and the handler for 'PageBack':
```
                if (msg.ButtonName.Equals("PageNext"))
                    ChangePage(true, msg.Sender.Name);
```


### Sample Code Documents
A number of sample PDF documents are included in the sdk distribution.

### Sample Code Keyboards
- virtual keyboard definitions
As described for the [Server keyboards](#server-keyboards)

### Sample Code Media
- images and video for the Idle mode slideshow
As described for the [Server Media](#server-media)

---

