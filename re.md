# Otravo

## About me
Alexander Cheprasov
- email: acheprasov84@gmail.com
- phone: 07490 216907
- linkedin: https://uk.linkedin.com/in/alexandercheprasov/
- CV: http://cheprasov.com/cv.pdf
- London, UK

## About JSquery test

Please, see result of the test in file `JSquery_result.js`

How to run: `node ./JSquery_result.js`

## About Tickets4Safe test

First of all, I want to notice that the phrase `Ticket sale starts 25 days before a show starts;` means that the show date included to the period. (see explanation below)

### Explanation of "Ticket sale starts 25 days before a show starts;"

I am writing about it, because I have 1 logical question. I will ask it later.

It is important for me, because in Russian language the phrase means, that the show date is not includes in the period `25 days before a show starts`. And I was a little confused about examples, in the test.

I will try to describe it more detailed.

For example, we have next show (Scenario 2):

Everyman, 2017-08-01, drama

Running the program with the above inventory, query-date 2017-08-01, and show-date 2017-08-15 should give:

Result that we have in the test:
```json
{
    "title": "everyman",
    "tickets left": "100", // 100 sold (200 cap - 100 left)
    "tickets available": "10",
    "status": "open for sale"
}
```

Now, we can see, that on query date 2017-08-01:
- left 100 tickets (sold 100 for prev days) in Tab 1
- left 90 tickets (sold 110 for prev days) in Tab 2

Yep, it is looks fine for 2 languages.

Ok, now I asked the question that confused me:
```
If show starts on 2017-08-15 and ticket sale starts 1 day before a show starts,
what is the firts date when people can buy tickets?
```
For me, it looks like:

2017-08-15 - 1 day = 2017-08-14

##### Tab1. English variant (implemented in the test)

Days before start show | Query Date | Left | Sold tickets for end of the day
---|---|---|---
25 | 2017-07-22 | 200 | 10
24 | 2017-07-23 | 190 | 20
23 | 2017-07-24 | 180 | 30
22 | 2017-07-25 | 170 | 40
21 | 2017-07-26 | 160 | 50
20 | 2017-07-27 | 150 | 60
19 | 2017-07-28 | 140 | 70
18 | 2017-07-29 | 130 | 80
17 | 2017-07-30 | 120 | 90
16 | 2017-07-31 | 110 | 100
15 | 2017-08-01 | 100 | 110
14 | 2017-08-02 | 90 | 120
13 | 2017-08-03 | 80 | 130
12 | 2017-08-04 | 70 | 140
11 | 2017-08-05 | 60 | 150
10 | 2017-08-06 | 50 | 160
9 | 2017-08-07 | 40 | 170
8 | 2017-08-08 | 30 | 180
7 | 2017-08-09 | 20 | 190
6 | 2017-08-10 | 10 | 200 / sold
5 | 2017-08-11 | 0 | 200 / sold
4 | 2017-08-12 | 0 | 200 / sold
3 | 2017-08-13 | 0 | 200 / sold
2 | 2017-08-14 | 0 | 200 / sold
1 (show date) | 2017-08-15 | 0 |

##### Tab2. Russian variant

in Russian language the phrase means, that the show date is not includes in the period `25 days before a show starts`.

Days before start show | Query Date | Left | Sold tickets for end of day
---|---|---|---
25 | 2017-07-21 | 200 | 10
24 | 2017-07-22 | 190 | 20
23 | 2017-07-23 | 180 | 30
22 | 2017-07-24 | 170 | 40
21 | 2017-07-25 | 160 | 50
20 | 2017-07-26 | 150 | 60
19 | 2017-07-27 | 140 | 70
18 | 2017-07-28 | 130 | 80
17 | 2017-07-29 | 120 | 90
16 | 2017-07-30 | 110 | 100
15 | 2017-07-31 | 100 | 110
14 | 2017-08-01 | 90 | 120
13 | 2017-08-02 | 80 | 130
12 | 2017-08-03 | 70 | 140
11 | 2017-08-04 | 60 | 150
10 | 2017-08-05 | 50 | 160
9 | 2017-08-06 | 40 | 170
8 | 2017-08-07 | 30 | 180
7 | 2017-08-08 | 20 | 190
6 | 2017-08-09 | 10 | 200 / sold
5 | 2017-08-10 | 0 | 200 / sold
4 | 2017-08-11 | 0 | 200 / sold
3 | 2017-08-12 | 0 | 200 / sold
2 | 2017-08-13 | 0 | 200 / sold
1 | 2017-08-14 | 0 | 200 / sold
0 (show date) | 2017-08-15 | 0 | 


