# infzadanie4.3

def count_deletions(word):
    if word == "wakacje":
        return 0
    
    target_word = "wakacje"
    word_length = len(word)
    target_length = len(target_word)
    
    dp = [[0] * (target_length + 1) for _ in range(word_length + 1)]
    
    for i in range(1, word_length + 1):
        for j in range(1, target_length + 1):
            if word[i - 1] == target_word[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
    
    return word_length + target_length - 2 * dp[word_length][target_length]

result = []
with open('slowo.txt', 'r') as file:
    for line in file:
        word = line.strip()
        deletions = count_deletions(word)
        result.append(deletions)

with open('wyniki4_3.txt', 'w') as output_file:
    output_file.write(' '.join(map(str, result)))
