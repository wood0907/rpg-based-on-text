# rpg-based-on-text
import random
    if choice == "1":
        return "전사"
    elif choice == "2":
        return "궁수"
    elif choice == "3":
        return "마법사"
    else:
        print("잘못 선택했습니다. 기본 직업: 전사")
        return "전사"


# =============================
# Battle System
# =============================
def battle(player, enemy):
    print(f"\n⚔️ {enemy.name} 등장!")

    while player.is_alive() and enemy.is_alive():
        print(f"플레이어 HP: {player.hp}")
        print(f"적 HP: {enemy.hp}")

        input("엔터를 눌러 공격하세요...")

        # Player attack
        damage = random.randint(player.attack - 3, player.attack + 3)
        enemy.hp -= damage
        print(f"플레이어가 {damage} 데미지를 입혔습니다!")

        if enemy.is_alive():
            damage = random.randint(enemy.attack - 2, enemy.attack + 2)
            player.hp -= damage
            print(f"적이 {damage} 데미지를 입혔습니다!")

    if player.is_alive():
        print("\n승리했습니다!")
        get_item()
        return True
    else:
        print("\n패배했습니다...")
        return False


# =============================
# Item Drop System
# =============================
def get_item():
    items = ["전설 무기", "희귀 무기", "일반 무기", "회복 포션"]
    chances = [1, 9, 30, 60]

    item = random.choices(items, weights=chances)[0]

    print(f"🎁 아이템 획득: {item}")


# =============================
# Game Loop
# =============================
def main():
    print("=== 로그라이크 RPG 게임 시작 ===")

    job = choose_weapon()
    player = Player(job)

    print(f"당신의 직업은 {player.job} 입니다!")

    stage = 1

    while True:
        print(f"\n===== 스테이지 {stage} =====")
        enemy = Enemy(stage)

        win = battle(player, enemy)

        if not win:
            print("게임 오버")
            break

        stage += 1


if __name__ == "__main__":
    main()
