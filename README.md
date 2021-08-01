This is a collection of things I've learnt for Minecraft modding, specifically using [Fabric](https://fabricmc.net/wiki/doku.php). I'm making this because I've found there isn't a lot of information for anything more than the basics. These have only been tested for 1.17.1

## Teleport Entity to Dimension
To teleport an entity to the Overworld, Nether or End:
1. Get the destination with `World.`DESTINATION
  * `World.END`
  * `World.NETHER`
  * `World.OVERWORLD`
2. Pass it into MinecraftServer`.getWorld()`
3. Pass that result into Entity`.moveToWorld()`

```java
// This teleports the player to the End
// player is a ServerPlayerEntity
player.moveToWorld(player.server.getWorld(World.END));
```

## Knockback Item
```java
import net.minecraft.entity.LivingEntity;
import net.minecraft.item.Item;
import net.minecraft.item.ItemStack;

public class KnockbackItem extends Item {

    public KnockbackItem(Settings settings) {
        super(settings);
    }

    @Override
    public boolean postHit(ItemStack stack, LivingEntity target, LivingEntity attacker) {
        int knockbackStrength = 4; // make this whatever you want
        target.takeKnockback(knockbackStrength, attacker.getX() - target.getX(), attacker.getZ() - target.getZ());
        return true;
    }

}
```
