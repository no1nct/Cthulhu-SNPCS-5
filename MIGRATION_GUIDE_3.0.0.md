# Cthulhu SNPCs - VJ Base 3.0.0 Migration Guide

This document outlines the changes made to upgrade this addon from VJ Base 2.x to 3.0.0.

## Major Breaking Changes Applied

### 1. **Sound System Overhaul**
- **Old**: Sound system had map cutoff limitations
- **New**: New sound system works across map in multiplayer
- **Changes**: Sound tables remain similar but reorganized internally
- **Files Affected**: All NPC init.lua files

### 2. **Animation System (CRITICAL)**
- **Old**: Used `vjges_` and `vjseq_` tags separately with different handling
- **New**: Unified animation system - sequences and activities use same system
- **Changes**:
  - Animation transitions now smoother
  - Added animation linking system
  - Aerial & Aquatic NPCs now use ground NPC animation system
- **Files Affected**: All NPC files with `AnimTbl_` variables

### 3. **Removed/Renamed Variables**

#### Completely Removed:
- `self.CurrentDeathSound` (replaced by GMod's system)
- `self.Tank_GunnerIsTurning`
- `self.NPC_HasSecondaryFireSound` (weapon base)
- `self.LastOwner` (weapon base)
- `self.InitHasIdleAnimation` (weapon base)

#### Renamed:
- `self.NextIdleSoundT_Reg` → `self.IdleSoundBlockTime`
- Sound timing variables now use unified format

### 4. **AI System Changes**
- New firing cone system for weapons
- New bullet spread system (distance, target movement, suppression-based)
- New grenade/projectile prediction system
- Attack priority system: `Custom → Melee → Range/Grenade → Leap`

### 5. **NPC Base Function Changes**

Removed/Deprecated:
- `self:GetNPCHealth()` / `self:GetNPCMaxHealth()` (use GMod's networked version)
- `self:AlertSoundCode()` (now integrated)
- `self:DeathSoundCode()` (now integrated)

New/Updated:
- `self:PlaySoundSystem(Set, CustomSd, Type)` - better sound handling
- `self.EnemyData` - merged enemy-related variables
- `self:Controller_Initialize(controlEnt)` - updated controller support
- `self.AttackStatus` and `self.AttackType` enums

### 6. **Corpse/Ragdoll System**
- Added velocity based on animation frames
- Localized bone velocity for bullet damage
- Better corpse collision handling

### 7. **Weapon System**
- NPCs now use proper RPM (rate of fire) system
- New firing cone requirement system
- Improved bullet spread calculation

## Files That Need Updates

### Priority 1 (Critical):
- `lua/entities/npc_vj_cthulhu_*/init.lua` - NPC definitions
- `lua/weapons/weapon_vj_cthulhu_*/shared.lua` - Weapon definitions

### Priority 2 (Important):
- `lua/effects/` - Effect definitions
- `lua/autorun/vj_cthulhu_autorun.lua` - Autorun file

## Migration Checklist

- [x] Updated death animation variables
- [x] Updated sound system calls
- [x] Removed deprecated weapon variables
- [x] Updated controller initialization
- [x] Added new animation system support
- [x] Updated entity data structures
- [ ] Test all NPCs in-game
- [ ] Test all weapons in-game
- [ ] Test animations and movement
- [ ] Test sound playback
- [ ] Test controller functionality

## Testing Recommendations

1. **Spawn NPCs** - Check for console errors
2. **Animation playback** - Verify death, idle, and attack animations
3. **Sound playback** - Check all sound files play correctly
4. **Weapon firing** - Test NPC weapon behavior
5. **Controller** - Test player NPC control
6. **Multiplayer** - Verify sounds work across map

## Need Help?

Refer to VJ Base 3.0.0 documentation and the official release notes for complete details on API changes.
