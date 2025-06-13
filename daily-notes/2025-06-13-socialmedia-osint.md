# OSINT is CRAZY – The Social Media Deep Dive

Till now, I always thought OSINT meant doing boring, manual searches for every tiny detail, and honestly, it felt kind of dull. But just now, when I started exploring **social media OSINT**, I realized how much we can actually track using free websites available online. We just need to log in, and we can find out a lot about someone.

---

## Twitter OSINT

I’m not a heavy Twitter user, but once I saw what’s possible with just a **username**, I was surprised. And if you somehow get their **Gmail**, the game levels up even more.

### Tools:

- **Socialbearing** / **Twitonomy**
  - Gives deep analytics of any public Twitter account
  - Shows post frequency, hashtags, common words, who they interact with
  - Can predict their sleep schedule from timestamps
  - Helps map their social circle

- **Spoonbill**
  - Tracks all profile changes: name, bio, profile pic, etc.
  - Shows every change made on the account over time

---

## Facebook OSINT

I don’t use Facebook much these days, but I still have an account. Facebook has tightened privacy settings, but it's still possible to extract data.

### Tricks:

- **Search for tagged photos**
  - Use: `photos of "name"`
  - Even if the account is private, photos they're tagged in by public accounts are visible
  - Metadata from those pics can reveal time, location, etc.

- **Download content and profile pics**
  - Tools:
    - `sowdust.github.io`
    - `intelx.io`
  - These allow downloading and analyzing content that Facebook normally restricts

---

## Instagram OSINT

This is the platform I use the most. I was hoping to find out who follows someone recently or who they talk to the most, like on Twitter, but Instagram is quite secure. Still, there are some useful tools.

### Tools:

- **Wopita.com**
  - Saves public data/pics from accounts before they went private
  - Lets you download all previously public posts

- **Codeofaninja.com**
  - Tracks Instagram username changes using user ID
  - User IDs never change, so if you save it, you can always track their new username

- **Imginn.com**
  - Downloads stories, profile pics, and posts from public accounts

---

## Snapchat OSINT

I never thought Snapchat could be useful in OSINT, but it actually has a unique feature.

- **map.snapchat.com**
  - A live map showing where public snaps are uploaded
  - Click any area to see recent snaps from that location
  - Useful for investigations if someone was at a known place and time

---

## Reddit OSINT

Reddit is more open like Twitter.

- All a person’s posts and comments are public (if you know the username)
- People often share personal opinions, locations, habits in discussions
- A great source to build a behavioral or psychological profile

---

## LinkedIn OSINT

This is highly underrated in OSINT but can reveal a lot.

- Users share:
  - Phone numbers, DOBs, emails
  - Resume, work history, certificates, education, etc.
- Even private accounts reveal info through search engine indexing and previews

Before, I used to think there’s no harm in someone knowing my certifications or where I studied, but now I realize very few people share my exact combination of details. That makes it easy to uniquely identify someone.

---

## Final Thoughts

That’s all for this blog. Next up, I’ll dive into **Web OSINT** and using **Kali tools** to automate this work instead of doing everything manually.

Still, manual searching has its own importance. Tools can fetch data, but only humans can connect the dots.
