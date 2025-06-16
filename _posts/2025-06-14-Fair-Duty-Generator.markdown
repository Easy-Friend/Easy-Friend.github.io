---
layout: post
title:  "FairDuty - Duty-Roster-Generator"
date:   2025-06-14 16:02:02 +0900
categories: projects
---
### My First Project
[FairDuty](https://fairduty.work)

### Reason of making it.

I ended up creating my first project - a duty roster generator that automatically generates duty schedules. I initially thought about making a profit out of it, but ran into issues with business registration(which was necessary for publishing an app in South Korea). So in a bit of an attention-seeking move, I decided to upload it here and there to drive some traffic. That's the real reason why I started this GitHub blog - to make it searchable on Google. I originally wanted this to be my first post. However, the process of making a blog was so challenging that the story of me struggling to set the GitHub blog became the first one. 

During my residency, I often had to create duty roster. And every department has its own complex rules of generating a duty schedule. In my case, we normally had two people on duty, but on Sundays, we needed three: two first-year residents and one third-year. Fourth-years were generally excluded from weekend shifts as a courtesy.

Now you might think, "How hard can making a roster be?". Sure enough, making a schedule for a week is doable. But once you start planning for a month or two, especailly around holidays like Lunar New Year or Chuseok, it becomes incredibly difficult to satisfy everyone.

At that point, the fairness is largely dependent on the very person who creates the schedule. If that someone puts a lot of thought and time into it, it can be quite fair but it might take up a huge chunk of their already limited time. In opposite case, unfair schedule will be made.

So I have been wondering - Is there anywone who would make a tool that could just one-click and generate the schedule? Since I have bunch of free time thesedays, I decided to make it on my own with the big-help of Gemini.

There were many times along the way when I felt like giving up and just calling it a "first-time hobby project", but thanks to my wife - who palyed the role of a demanding user - I was able to push through and build something that at least I would genuinely want to use.


### Feature highlights
There's honetly not much to explain. It's more about sharing my intentions and a bit of venting. I think I've managed to include pretty much all the input values I wanted.

1. The scheduling period
    - Right now, the maximum period you can generate a schedule for is 6 weeks. I originally wanted to allow longer periods, but ran into a technical limitation: the backend is hosted on Heroku, which only processes requests within 30 seconds. If it takes longer, it throws a TimeoutError, and the frontend fails to retrieve the result properly.
    
    Sure, this could be solved by using a database and implementing some asynchronous job processing. But since I’m not making any money from this project, I wanted to keep running costs as low as possible. So I had to place a limit on both the scheduling period and the number of people that can be included.

2. Extra holidays / no duty days
    - At first, I only had a feature to mark additional holidays, aside from weekends. I originally wanted to pull public holiday data by country and treat them like weekends automatically. But there were just too many exceptions—substitute holidays, foundation days, and other custom off-days—so I ended up letting users manually select holidays instead.

    Then someone asked me, “What about days when no one has to be on duty at all?”
    And to be honest, as someone still mentally shackled by the system, my first thought was:
        “What do you mean, no one on duty? Then who’s going to cover that day?”
    But apparently, people in other departments don’t need weekend duties sometimes—so I added that option too.

    Initially, adding multiple separate inputs for all of this made the UI messy. Too many date pickers slowed things down and looked cluttered. So I implemented a double-click feature instead:
    One click marks a holiday (bad mood = red)
    A second click marks a no-duty day (good mood = green)
    Honestly, that small UI trick ended up being one of the things I’m most satisfied with.

    Later on, when I added the feature for “mandatory duty days,” I just reused the same double-click mechanism.

3. Number of people on duty
    - Of course, this was one of the very first features I implemented—because deciding how many people should be on duty is kind of essential.
    At first, I skipped more complex patterns like varying the number of people per day (e.g., different numbers on different dates), telling myself:
    “Eh... do we really need that level of complexity?”
    But—well—you know how it goes. I ended up adding it anyway.

4. Consecutive duty days
    - This refers to doing duty shifts on consecutive days, something that’s technically not allowed (or at least, shouldn’t be). But in reality? It still happens all the time.
    Because let’s be honest—
    “If everyone leaves, who’s going to run the hospital?”
    So yes, back-to-back duty is still a thing.
    Still, I believe that someone has to strive for a better system, so I set the default setting to disallow consecutive shifts.
    Let’s call it a small step toward a more humane scheduling future. 

5. Days with a different number of duty personnel 
    - From personal experience, there are certain days when things get especially hectic, and you simply need more people on duty. To be honest, I really didn’t want to implement this feature (reason: pure laziness). I tried hard to ignore the need for it. But then I asked myself: If even I wouldn’t use this site, what’s the point of building it? So yeah, I gave in. If I want to use it, I need this feature too.
    I wasn’t sure at first how to design the input for it, but thankfully, my very demanding (and very helpful) wife suggested a great solution: Just show an extra datepicker for these "special days", and for each date selected, let the user input how many people should be assigned. Turns out, it’s actually the most intuitive and elegant approach. So I went with it—and I’m pretty happy with the result.

6. People on duty
    - This one’s a no-brainer. Of course, you need to input who’s available to be scheduled. The UI lets you add people just by hitting Enter, which felt like the simplest and most intuitive way. You can also remove anyone as needed. I did consider adding a “delete all” button... but then reminded myself that this isn’t a data-saving site. Just hit refresh. Boom. Everyone’s gone. Problem solved. So yeah—I ignored that one.

7.  Days people can’t or must be on duty
    - This feature was also essential—because let’s face it, if I’m making a tool for myself, it can’t violate the sacred rule that:
    Fourth-years do not take weekend duties. At first, I didn’t plan to support mandatory duty days, but then I realized I could reuse the double-click UI logic from before. It doesn’t clutter the interface, and it adds a surprisingly useful feature. For example, big holidays like Chuseok or Lunar New Year often involve careful planning to let people go home—so manually marking someone as required on those days makes perfect sense.
    And honestly? It works pretty smoothly.


### Stuff I could have added, but didn’t… yet
1.  Viewing previously generated schedules. Honestly, I never even thought of this feature. It was actually my wife’s idea (again). But yeah... I didn’t want to set up a database. Right now, generating a schedule still feels a bit like rolling dice—you just keep hitting the button until something decent comes out. But later, you might find yourself thinking: “Ugh, the last one was better…”. So yeah, being able to view the previous result would be nice. I’m considering temporarily saving the last result and showing it again... maybe. Anyway, my stubborn refusal to add this feature is what led me to implement the download button instead.

2. Export to Excel - This one’s just... pure laziness on my part. In reality, people often need to submit the schedule somewhere, even just for show—so an Excel export feature would be useful. But I justified skipping it with this logic: “You can just copy and paste the table into Excel—it works fine.” So yeah... no export button (for now).

### A few things I did focus on (even if I don’t fully understand the math…)
My math background isn’t exactly strong, and I can't pretend I fully understand all the code that AI helped me write,
but I did have a few principles I wanted the program to follow:

1. This was the core goal from the start. If the schedule isn’t fair, there’s really no point in using it.
 - At first, I tried a simple logic: Fix the number of weekend duties per person. Then distribute the weekdays. But it turned out that even after 100 iterations, there were often 2 or more weekday duties difference between people, which felt unfair way too often. So I changed the approach entirely: First, find the minimum possible number of weekday/weekend duties per person that satisfies the constraints (usually just 1 or 2 each). Then, generate 50–70 combinations that meet that target.Finally, pick the combination with the lowest overall variance. That’s how the final schedule gets selected.

2. Spread out the duties (no clumping)
 - This was one of the last features I added.
Among all valid results, I try to minimize the clustering of duty days per person, so no one ends up doing all their shifts in one intense week.

And… that’s the end of my first dev project write-up.
May your schedules be fair, your duties light, and your backups always work. Thanks for reading