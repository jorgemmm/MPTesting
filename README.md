# MP Testing
This Unreal Engine C++ source project is for Multipayer features testing
You can test with NULL subsystem how to create a session and how to join to it trough the LAN

The porposes of this little project is didact, is learn like a Hello world about
creation an join session trough LAN

If you wanna use internet you'll need steam or EOS subsystem

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

## Installation
1. You Clone the repository:
```bash
 git clone https://github.com/yourusername/yourproject.git
```
but I think is better idea only copy the 3 method and 
paste it in your character class.

```bash
//.h
UFUNCTION(BlueprintCallable)
void OpenLobby();
UFUNCTION(BlueprintCallable)
void CallOpenLevel(const FString& Address);
UFUNCTION(BlueprintCallable)
void CallclientTravel(const FString& Address);

//.cpp
void AMPTestingCharacter::OpenLobby()
{
  UWorld* World = GetWorld();
  if(!World)
  {
    UE_LOG(LogTemp, Error, TEXT("World is nullptr not posible servertravell"));
    return;
  }	
  if(!World->ServerTravel("/Game/ThirdPerson/Maps/Lobby?listen")  )
  {
    UE_LOG(LogTemp, Error, TEXT("server not open lobby, Can´t travel to lobby"));
  }
}

void AMPTestingCharacter::CallOpenLevel(const FString& Address)
{
  UGameplayStatics::OpenLevel(this, *Address);
}

void AMPTestingCharacter::CallclientTravel(const FString& Address)
{
  APlayerController* PlayerController = GetGameInstance()->GetFirstLocalPlayerController();
  if(!PlayerController)
{
  UE_LOG(LogTemp, Error, TEXT("playercontroller is nullptr and then client Can´t be able travel to lobby"));	
  return;
}
  PlayerController->ClientTravel(Address, ETravelType::TRAVEL_Absolute);
}

```
Address is the IP address of the Host, where you has created the session.
You can find out easyly which is your ip with CMD command > ipconfig
2. Install dependencies:
```bash
 You need Visual studio and unreal engine
 ```

## Usage

Create project with third person character
and create another map y maps folder, lobby.

You can use other names and your own project but you have to change the path in OpenLobby():


In Your character, **in blueprint** call this method with inputs events. 
Example:
1.  press 1 -> CallOpenLobby()
2.  press 2 -> CallOpenLevel(HostIPadress)
3.  press 3 -> call CallclientTravel(HostIPadress)

You could choose your development equip like host PC... and find fastly the HostIPadress with ipcongig cmd comand.

Build the project. Upload to google drive. ( a third person character template <2G) and download in as many PCs as you can .

Run game in all PC

In your PC lobby ( it must be ipadres=HostIPadress ) Create a lobby. press 1.

In any other pc press 2 or press 3...Wath happen??

In your own:
You can change callopenlobby for .
```bash
CallOpenLobby(const* FString PathToLobby)
Path="/Game/ThirdPerson/Maps/Lobby?listen" 
if PathToLobby!="" :
  Path = PathToLobby+"?listen"
 UWorld* World = GetWorld();
  if(!World)
  {
    UE_LOG(LogTemp, Error, TEXT("World is nullptr not posible servertravell"));
    return;
  }	
  World->ServerTravel(Path) 
```
In this way, the lobby route is exposed in the blueprint. if you don´t write anything... load default lobby
## License
This project is licensed under the [MIT License](https://mit-license.org/).

