## Installieren


```mermaid
graph TD
    A[ASP.NET Core Installation] --> B[.NET SDK herunterladen]
    B --> C[.NET SDK installieren]
    C --> D[Visual Studio Code installieren]
    D --> E[Visual Studio Code Erweiterungen installieren]
    E --> F[Entity Framework Installieren]
    F --> G[Anwendung herunderladen]

```

## .NET SDK installieren
Öffne Sie das Terminal und auf ihrem Ubuntu-Desktop
```bash
sudo apt-get update 
sudo apt-get upgrade
sudo apt-get update # Aktualisiert die Paketliste
sudo apt-get install -y dotnet-sdk-9.0 # Installation des .NET SDK
sudo apt-get install -y dotnet-sdk-8.0 # Installation des .NET SDK
echo 'export PATH=$HOME/.dotnet/tools:$PATH' >> ~/.bashrc # Hinzufügen des Pfads zum .bashrc
source ~/.bashrc  # Aktualisierung der .bashrc
```
### Warum beide Versionen von .NET Core?

Softwaremodule sind nicht immer vollständig kompatibel.
## Visual Studio Code Installieren
```bash 
sudo snap install code --classic
```
## Visual Studio Code Erweiterung Installieren
```
code --install-extension ms-dotnettools.csdevkit # Installiert die C# Dev Kit Erweiterung
```
## Entity Framework Installieren
```bash
dotnet tool install --global dotnet-ef
```

## Anwendung herunterladen
```bash
git clone https://github.com/thorstenkloehn/aspnetcoremvc.git
![type:video](https://www.youtube.com/embed/LXb3EKWsInQ)

