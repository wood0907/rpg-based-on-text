import random

# ---------- 플레이어 ----------
class Player:
    def __init__(self, job):
        self.job = job

        if job == "전사":
            self.hp = 120
            self.attack = 15
        elif job == "궁수":
            self.hp = 100
            self.attack = 18
        elif job == "마법사":
            self.hp = 80
            self.attack = 22

    def is_alive(self):
        return self.hp > 0


# ---------- 몬스터 ----------
class Enemy:
    def __init__(self, stage):
        self.name = f"슬라임 (Stage {stage})"
        self.hp = 40 + stage * 10
        self.attack = 8 + stage * 2

    def is_alive(self):
        return self.hp > 0


# ---------- 직업 선택 ----------
def choose_weapon():
    print("무기를 선택하세요")
    print("1. 검 (전사)")
    print("2. 활 (궁수)")
    print("3. 지팡이 (마법사)")

    choice = input("> ")

    if choice == "1":
        return "전사"
    elif choice == "2":
        return "궁수"
    elif choice == "3":
        return "마법사"
    else:
    

# ---------- 아이템 드랍 ----------
def get_item():
    items = ["전설 무기", "희귀 무기", "일반 무기", "회복 포션"]
    chances = [1, 9, 30, 60]

    item = random.choices(items, weights=chances)[0]

    print(f"아이템 획득: {item}")


# ---------- 전투 ----------
def battle(player, enemy):
    print(f"\n{enemy.name} 등장!")

    while player.is_alive() and enemy.is_alive():
        print("-------------------")
        print(f"플레이어 HP: {player.hp}")
        print(f"적 HP: {enemy.hp}")

        input("엔터를 누르면 공격합니다...")

        # 플레이어 공격
        damage = random.randint(player.attack - 3, player.attack + 3)
        enemy.hp -= damage
        print(f"플레이어 공격! {damage} 데미지")

        if enemy.is_alive():
            damage = random.randint(enemy.attack - 2, enemy.attack + 2)
            player.hp -= damage
            print(f"적 공격! {damage} 데미지")

    if player.is_alive():
        print("승리!")
        get_item()
        return True
    else:
        print("패배...")
        return False


# ---------- 게임 시작 ----------
def main():
    print("=== RPG 게임 시작 ===")

    job = choose_weapon()
    player = Player(job)

    print(f"당신의 직업: {player.job}")

    stage = 1

    while True:
        print(f"\n===== Stage {stage} =====")

        enemy = Enemy(stage)

        win = battle(player, enemy)

        if not win:
            print("게임 오버")
            break

        stage += 1


# 프로그램 시작 지점
if __name__ == "__main__":
    main()

