uintptr_t GNames = 0x6eb8b00;
uintptr_t GObjects = 0x6ed12d8;
uintptr_t GWorld = 0x700fdd0;
constexpr auto PersistentLevel = 0x30; // ULevel*
constexpr auto OwningGameInstance = 0x188; // UGameInstance*
constexpr auto LocalPlayers = 0x38; // TArray<ULocalPlayer*>
constexpr auto PlayerController = 0x30; // APlayerController*
constexpr auto AcknowledgedPawn = 0x2b0; // APawn*
constexpr auto PlayerCameraManager = 0x2c8; // APlayerCameraManager*
constexpr auto OwningActor = 0x98; // AActor*
constexpr auto MaxPacket = 0xa0; // int32_t
constexpr auto RootComponent = 0x138; // USceneComponent*
constexpr auto RelativeLocation = 0x124; // FVector
constexpr auto CamCache = 0x1af0; // FCameraCacheEntry
 
 
 
uint64_t uworld = Read<uint64_t>(base_address + offsets::GWorld);
uint64_t persistentlvl = Read<uint64_t>(uworld + offsets::PersistentLevel);
uint64_t gameinstance = Read<uint64_t>(uworld + offsets::OwningGameInstance);
uint64_t localplayer = Read<uint64_t>(gameinstance + offsets::LocalPlayers);
uint64_t localplayers = Read<uint64_t>(localplayer);
playercontroller = Read<uint64_t>(localplayers + offsets::PlayerController);
camera_manager = Read<uint64_t>(playercontroller + offsets::PlayerCameraManager);
uint64_t actor_array = Read<uint64_t>(persistentlvl + offsets::OwningActor);
int actor_count = Read<int>(persistentlvl + offsets::MaxPacket);
FCameraCacheEntry camera_cache = Read<FCameraCacheEntry>(camera_manager + offsets::CamCache);
for (unsigned long i = 0; i < actor_count; ++i)
{
 
 uint64_t actor = Read<uint64_t>(actor_array + i * 0x8);
 if (actor == 0x00)
 {
	continue;
 }
 
 
int id = Read<int>(actor + 0x18);
 
std::string namedump = GetNameFromFName(id);
std::cout << "name dump : " << namedump << std::endl;
 
uint64_t rootcomponent = Read<uint64_t>(actor + offsets::RootComponent);
Vector3 relativelocation = Read<Vector3>(rootcomponent + offsets::RelativeLocation);
Vector3 cizpic = worldtoscreen(relativelocation, camera_cache.POV);
DrawStrokeText(cizpic.x, cizpic.y, &Col.red, "lol");
 
}
