#include <vip_core>
#include <sdktools>
#include <sdkhooks>

public Plugin myinfo = {
	name = "[VIP] Fire Grenade",
	description = "",
	author = "Mozze",
	version = "1.1",
	url = "t.me/pMozze"
};

public void OnPluginStart() {
	if (VIP_IsVIPLoaded())
		VIP_RegisterFeature("FireGrenade", BOOL);
}

public void OnPluginEnd() {
	if (CanTestFeatures() && GetFeatureStatus(FeatureType_Native, "VIP_UnregisterFeature") == FeatureStatus_Available)
		VIP_UnregisterFeature("FireGrenade");
}

public void VIP_OnVIPLoaded() {
	VIP_RegisterFeature("FireGrenade", BOOL);
}

public void OnEntityCreated(int iEntity, const char[] szClassName) {
	if (StrEqual(szClassName, "hegrenade_projectile"))
		CreateTimer(0.1, onGrenadeSpawned, iEntity);
}

public Action onGrenadeSpawned(Handle hTimer, int iEntity) {
	if (IsValidEntity(iEntity) && IsValidEdict(iEntity) && HasEntProp(iEntity, Prop_Send, "m_hThrower")) {
		int iThrower = GetEntPropEnt(iEntity, Prop_Send, "m_hThrower");

		if (iThrower && IsClientInGame(iThrower) && (VIP_IsClientVIP(iThrower) && VIP_IsClientFeatureUse(iThrower, "FireGrenade")))
			IgniteEntity(iEntity, 5.0);
	}

	return Plugin_Stop;
}
