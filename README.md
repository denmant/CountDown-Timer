# CountDown-Timer

 //Calculating the Time Remaining
To calculate the time remaining, we need to find the difference between the current time and the time that our countdown timer will expire. One of the more notable times that we countdown to is New Year’s Day, so we’ll use the upcoming new year as our end time:

const difference = +new Date("2020-01-01") - +new Date();
The + before the new Date is shorthand to tell JavaScript to cast the object as an integer, which gives us the object’s Unix time stamp represented as microseconds since the epoch.

//Formatting to Days, Hours, Minutes and Seconds
Now that we know the total number of milliseconds until the countdown time expires, we need to convert the number of milliseconds to something a bit more friendly and human readable.

We’re going to calculate the total number of hours, minutes and of course, seconds, by doing some math and using the modulus % operator:

const parts = {
  days: Math.floor(difference / (1000 * 60 * 60 * 24)),
  hours: Math.floor((difference / (1000 * 60 * 60)) % 24),
  minutes: Math.floor((difference / 1000 / 60) % 60),
  seconds: Math.floor((difference / 1000) % 60),
};
By rounding the numbers down, we’re able to drop the remainder to get the whole number value.

With an object full of the days, hours, minutes and seconds remaining, we can put things together into a string:

const remaining = Object.keys(parts)
  .map((part) => {
    if (!parts[part]) return;
    return `${parts[part]} ${part}`;
  })
  .join(" ");

//Show the Time Remaining on the Page
With the time parts assembled into a string, we can update our <div> to contain the value:

document.getElementById("countdown").innerHTML = remaining;
Automatically Updating the Timer
Thus far, we’ve calculated the time difference between the current time and the time that our countdown expires. We’ve broken that time into hours, minutes and seconds, and then updated the page with the time remaining.

Then time stood still.

Without additional logic to update the page periodically, the timer is stuck in place until the next time the page is loaded. Without an update, it’s hard to even describe it as a timer.

No big deal, we can easily create an interval to run every second (or 1000ms) and update the timer’s display:

setInterval(() => {
  // This is where we'd recalculate the time remaining
}, 1000);
