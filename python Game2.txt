#pseudo-code --> code
import random

#ตัวแปรที่ระบุสถานะของเกม
score = 0
lives = 3
words = ['title','grace','palm']

def update_clue(guess, secret_word, clue):
    #guess ไล่ไปทีละตัวอักษรใน secret_word ดูว่ามีตัวไหนบ้างตรงกับที่ทาย
    for i in range(len(secret_word)):
        #ถ้าทายตรงตัวไหน ก็อัพเดต clue  ตรงตำแหน่งนั้น
        if guess == secret_word[i]:
            clue[i] = guess
    win = ''.join(clue) == secret_word
    return win #ทายจนไม่เหลือ '?' แล้ว --> True, ยังเหลือ --> False

#ตราบใดที่ยังมีคำให้ทายอยู่ และ ชีวิตยังเหลือ --> เล่นต่อไป
while (len(words) > 0) and (lives > 0):
    #สุ่มคำจาก words แล้วดึงคำนั้นออกจาก list
    random.shuffle(words)
    secret_word = words.pop()
    clue = list('?'*len(secret_word)) #จน=ตัวอักษรของ secret_word

    #ตราบใดที่ยังทายคำนี้ไม่เสร็จหรือชีวิตยังไม่หมด
    while True:
        print(clue)
        print('ชีวิตที่เหลือ: ' + str(lives))
        guess = input('ทายตัวอักษรมาซิ: ')

        #check ว่าตัวอักษรที่ทาย อยู่ใน secret word ป่าว?
        if guess in secret_word:
            win = update_clue(guess, secret_word, clue)
            if win:
                print('เย้! คำนั้นก็คือ: '+secret_word)
                score = score + 1
                print('score: ' + str(score))
                break # ทายคำนี้เสร็จแล้ว
        else: #ที่ guess มา ไม่อยู่ใน secret_word
            print('ผิด! เลือดลด')
            lives = lives - 1
            if lives == 0:
                print('คุณแพ้แล้ว! คำนั้นคือ: ' + secret_word)
                break #ม่งเท่งแล้ว


print('Final score: ' + str(score))
print('Game end!')
