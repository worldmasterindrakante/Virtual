# Virtual World RPG Game - Base Structure
# This is a starter code concept using Python-like pseudocode for logic.
# For real game development, it can be implemented in Unity (C#) or Godot (GDScript)

# ----------------------------
# Character System
# ----------------------------
class Character:
    def __init__(self, name, gender, origin_story):
        self.name = name
        self.gender = gender
        self.origin_story = origin_story
        self.level = 1
        self.exp = 0
        self.money = 100
        self.inventory = []
        self.stats = {
            'strength': 5,
            'intellect': 5,
            'charisma': 5,
            'agility': 5,
            'soul_power': 0
        }
        self.is_rogue = False

    def gain_exp(self, amount):
        self.exp += amount
        if self.exp >= self.level * 100:
            self.level += 1
            self.exp = 0
            print(f"{self.name} leveled up to {self.level}!")

    def receive_damage(self, damage):
        # Placeholder health/damage logic
        pass

    def die(self, killer):
        stolen_money = int(self.money * 0.9)
        killer.money += stolen_money
        self.money -= stolen_money
        print(f"{killer.name} killed {self.name} and stole {stolen_money} coins!")

# ----------------------------
# Switcher - Admin AI System
# ----------------------------
class Switcher:
    def __init__(self, owner_username):
        self.owner = owner_username
        self.secret_phrase = "Together we are we will"

    def respond(self, username, phrase, question):
        if username == self.owner and phrase == "It's the world master — Together we are we will":
            return f"[Switcher] Response to: {question}"
        return "Access Denied."

# ----------------------------
# World Zones
# ----------------------------
class Zone:
    def __init__(self, name, danger_level=0):
        self.name = name
        self.danger_level = danger_level
        self.pvp_enabled = True if danger_level > 0 else False

origin_grounds = Zone("Origin Grounds", danger_level=0)
soul_city = Zone("Soul City", danger_level=1)
echo_woods = Zone("Echo Woods", danger_level=2)
demon_rift = Zone("Demon Rift", danger_level=3)
memory_isles = Zone("Memory Isles", danger_level=0)
forgotten_sky = Zone("Forgotten Sky", danger_level=4)

# ----------------------------
# PvP & Rogue System
# ----------------------------
def handle_pvp(attacker, defender, zone):
    if zone.pvp_enabled:
        defender.die(attacker)
        if defender.level < attacker.level - 3:
            attacker.is_rogue = True
            print(f"{attacker.name} is now marked as a Rogue Soul!")
    else:
        print("Combat not allowed in this zone.")

# ----------------------------
# Timer System
# ----------------------------
def game_start_timer():
    print("To a new beginning")

# ----------------------------
# Sample Game Flow
# ----------------------------
if __name__ == "__main__":
    game_start_timer()

    # Characters
    player1 = Character("Indrakante Sai Sreepadh", "Male", "Fallen Prince")
    player2 = Character("ShadowHunter", "Male", "Wanderer")

    # Switcher
    switcher = Switcher("Indrakante Sai Sreepadh")
    print(switcher.respond("Indrakante Sai Sreepadh", "It's the world master — Together we are we will", "Where is the Memory Isle?"))

    # Simulate PvP in Demon Rift
    handle_pvp(player1, player2, demon_rift)

    # Show player states
    print(f"{player1.name} - Money: {player1.money}")
    print(f"{player2.name} - Money: {player2.money}")
