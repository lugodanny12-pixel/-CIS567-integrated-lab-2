# -CIS567-integrated-lab-2
Week 7 Assignment
# Find highest score
def find_high_score(values):
    high_score = 0

    # Step 1: check singles (1-6)
    for goal in range(1, 7):
        high_score = max(high_score, check_singles(values, goal))

    # Step 2: check three, four, five of a kind
    high_score = max(high_score, check_three_of_kind(values))
    high_score = max(high_score, check_four_of_kind(values))
    high_score = max(high_score, check_five_of_kind(values))

    # Step 3: check full house
    high_score = max(high_score, check_full_house(values))

    # Step 4: check straight
    high_score = max(high_score, check_straight(values))

    return high_score

# Add all occurrences of goal value
def check_singles(dice, goal):
    return sum(value for value in dice if value == goal)

# Check for three of a kind (score = 30)
def check_three_of_kind(dice):
    for i in range(3):
        if dice[i] == dice[i+1] == dice[i+2]:
            return 30
    return 0

# Check for four of a kind (score = 40)
def check_four_of_kind(dice):
    for i in range(2):
        if dice[i] == dice[i+1] == dice[i+2] == dice[i+3]:
            return 40
    return 0

# Check for five of a kind (score = 50)
def check_five_of_kind(dice):
    if dice[0] == dice[1] == dice[2] == dice[3] == dice[4]:
        return 50
    return 0

# Check for full house (score = 35)
def check_full_house(dice):
    # Three + two pattern (sorted)
    if (dice[0] == dice[1] == dice[2] and dice[3] == dice[4]) or \
       (dice[0] == dice[1] and dice[2] == dice[3] == dice[4]):
        return 35
    return 0

# Check for straight (score = 45)
def check_straight(dice):
    if dice == [1, 2, 3, 4, 5] or dice == [2, 3, 4, 5, 6]:
        return 45
    return 0

if __name__ == '__main__':  # Do not modify
    # Fill array with five dice from input
    dice = [int(val) for val in input().split()]

    high_score = 0

    # Place dice in ascending order
    dice.sort()

    # Find high score and output
    high_score = find_high_score(dice)

    print(f'High score: { high_score }')
