# Keysar v2

## Description

Wow! Aplet sent me a message... he said he encrypted it with a key, but lost it. Gotta go though, I have biology homework!

[Source](./chall.py) [Output](./out.txt)

Author: EvilMuffinHa

## Approach

Using [Boxentriq](https://www.boxentriq.com/code-breaking/cipher-identifier), it identified the most likely ciphers it could be. It was a monoalpahbetical substitution cipher which is to say each letter of the alphabet is replaced with another letter in the cipher. I used [dcode](https://www.dcode.fr/monoalphabetic-substitution) to decode the cipher manually....

The cipher was the Bee Movie script with the flag appended at the end (I used [this website](https://convertcase.net/) to convert it to lowercase):

```text
according to all known laws of aviation, there is no way a bee should be able to fly. its wings are too small to get its fat little body off the ground. the bee, of course, flies anyway because bees don't care what humans think is impossible. yellow, black. yellow, black. yellow, black. yellow, black. ooh, black and yellow! let's shake it up a little. barry! breakfast is ready! coming! hang on a second. hello? barry? adam? can you believe this is happening? i can't. i'll pick you up. looking sharp. use the stairs. your father paid good money for those. sorry. i'm excited. here's the graduate. we're very proud of you, son. a perfect report card, all b's. very proud. ma! i got a thing going here. you got lint on your fuzz. ow! that's me! wave to us! we'll be in row 118,000. bye! barry, i told you, stop flying in the house! hey, adam. hey, barry. is that fuzz gel? a little. special day, graduation. never thought i'd make it. three days grade school, three days high school. those were awkward. three days college. i'm glad i took a day and hitchhiked around the hive. you did come back different. hi, barry. artie, growing a mustache? looks good. hear about frankie? yeah. you going to the funeral? no, i'm not going. everybody knows, sting someone, you die. don't waste it on a squirrel. such a hothead. i guess he could have just gotten out of the way. i love this incorporating an amusement park into our day. that's why we don't need vacations. boy, quite a bit of pomp... under the circumstances. well, adam, today we are men. we are! bee-men. amen! hallelujah! students, faculty, distinguished bees, please welcome dean buzzwell. welcome, new hive city graduating class of... ...9:15. that concludes our ceremonies. and begins your career at honex industries! will we pick ourjob today? i heard it's just orientation. heads up! here we go. keep your hands and antennas inside the tram at all times. wonder what it'll be like? a little scary. welcome to honex, a division of honesco and a part of the hexagon group. this is it! wow. wow. we know that you, as a bee, have worked your whole life to get to the point where you can work for your whole life. honey begins when our valiant pollen jocks bring the nectar to the hive. our top-secret formula is automatically color-corrected, scent-adjusted and bubble-contoured into this soothing sweet syrup with its distinctive golden glow you know as... honey! that girl was hot. she's my cousin! she is? yes, we're all cousins. right. you're right. at honex, we constantly strive to improve every aspect of bee existence. these bees are stress-testing a new helmet technology. what do you think he makes? not enough. here we have our latest advancement, the krelman. actf{keyedcaesarmorelikesubstitution}
```

## Flag

actf{keyedcaesarmorelikesubstitution}
