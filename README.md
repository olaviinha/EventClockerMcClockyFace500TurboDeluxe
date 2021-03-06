# EventClocker McClockyFace 500 Turbo Deluxe

EventClocker McClockyFace 500 Turbo Deluxe is an analogue clock web widget that displays today's events from a user-provided delimiter-separated txt file as arcs in its clockface. It can also display a list of upcoming and ongoing events.

Live demo: https://inha.asia/dmo/clocker/

Due to the maintainability, it is probably best suited for daily or weekly recurring events, but can also be used with one time events using dates.

I.e. it takes your data like this:
```
# Day & Time             Color   Description
daily 13:00-14:00;       #993;   Lunch
mon-fri 10:00-18:20;     #393;   Helsinki stock exchange is open
mon-fri 16:30-24:00;     -;      NYSE is open
tue-wed 14:00-18:00;     #99f;   Eduskunnan täysistunto
thu 16:00-20:00;         #99f;   Eduskunnan täysistunto
fri 13:00-17:00;         #99f;   Eduskunnan täysistunto
mon 18:00-19:00;         white;  Monday sauna
2021-08-22 18:30-20:00;  yellow; Ruusut @ Allas
2021-09-04 20:00-22:00;  yellow; The Hearing @ G Livelab
2021-11-23 19:00-23:00;  yellow; Igorrr @ Tavastia
``` 

...and turns it into something like this:
![image](https://user-images.githubusercontent.com/50331907/123425948-6c7ada00-d5cb-11eb-8640-fc11af48bf59.png)

...maybe this:
![image](https://user-images.githubusercontent.com/50331907/123425617-068e5280-d5cb-11eb-8f07-5f2a25e77855.png)

...or perhaps something like these:
![image](https://user-images.githubusercontent.com/50331907/122900624-8612ec00-d355-11eb-8bee-fd1b3944cc74.png)

---

### Prerequisites
- jQuery

### Setup

1. Place all files on a server.
2. Include required files in your website. Naturally you may compile the LESS file into a CSS file, or do your own styling.
```
  <link rel="stylesheet/less" type="text/css" href="clocker.less" />
  <script src="//cdnjs.cloudflare.com/ajax/libs/less.js/3.9.0/less.min.js" ></script>
  <script src="//ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
```
```
  <script src="clocker.js"></script>
```

3. Place EventClocker McClockyFace 500 Turbo Deluxe somewhere in your website.
```
  <div class="clocker"></div>
``` 
4. If you want to display the events as text, add also the following wrappers somewhere in your website. These templates are freely editable, just keep the class names the same as defined in `clocker.js`. By default these are `upcomings wrapper` and `ongoings wrapper` for the wrappers and `upcoming events` and `ongoing events` for the containers. Wrappers can contain any kind of content, such as titles in this example. Containers will list only the events. Wrappers can be hidden altogether if there is nothing in the container, and that will happen by default.
```
  <div class="upcomings wrapper">
    <strong>Coming up</strong>
    <div class="upcoming events"></div>
  </div>

  <div class="ongoings wrapper">
    <strong>Happening now</strong>
    <div class="ongoing events"></div>
  </div>
```
5. Replace events in `events.txt` with your own. You may also [host events.txt in Dropbox](#protip-host-eventstxt-in-dropbox-for-easy-updating) for easy updating.
6. Done.

### Settings

You can edit any of the settings in `clocker.js`:
```
// General settings
var events_txt = 'events.txt';                  // File containing your events in semicolon-separated format.
var clock_container = '.clocker';               // Element in which to place EventClocker McClockyFace itself.
var ongoing_wrapper = '.ongoings.wrapper';      // Wrapper element for ongoing events (parent of ongoing_container).
var upcoming_wrapper = '.upcomings.wrapper';    // Wrapper element for upcoming events (parent of upcoming_container).
var ongoing_container = '.ongoing.events';      // Element in which to list descriptions of ongoing events. Should be child of ongoing_wrapper.
var upcoming_container = '.upcoming.events';    // Element in which to list descriptions of upcoming events. Should be child of upcoming_wrapper.
var refresh_interval = 15;                      // Interval in minutes, in which events_txt is reloaded.

// Settings for events in clockface
var event_type = 'arcs';                        // 'lines', 'arcs' or 'both'. 'pie' is also available, but it's highly unuseful.
var start_lines_only = true;                    // When 'lines' or 'both' are displayed, display lines only for start times.
var hide_past_events = true;                    // Hide event from clockface when event has ended.
var events_opacity = 1;                         // Opacity of events on clockface
var randomize_colors = true;                    // Randomize colors daily for events that have no color defined. Colors are not changed during the day. true, false or 'light' (= same as true but lighter colors)
var default_color = 'rgb(1255,255,255)';        // Default color of events if randomize_colors is false and event has no color defined.

// Styling for arcs (when event_type is either 'arcs' or 'both')
var distance = .4;                              // Max distance of event from clock center. For aesthetics.
var separation = .06;                           // Gap (radial distance) between arcs. .03 = overlap; .07 = small gap; .1 = large gap.
var width = .25;                                // Arc thickness (radial width).
var rounded = false;                            // Arc ends are entirely rounded. Not suitable for thick arcs, as it adds half of line width as length to start and end.

// Settings for event list (event descriptions outside the clock itself)
var display_descriptions = true;                // Display lists of ongoing & upcoming events.
var hide_wrappers_when_empty = true;            // Hide wrappers when empty. Wrappers may contain titles and other content.
var show_upcoming_before = 1500;                // Show upcoming event description this many minutes before it starts. 1500 = list all today's events. 
var show_notification_before = 5;               // Show desktop notification this many minutes before event starts.
``` 

You can click clock to re-randomize colors.

### Events Data

In your events txt file, events should be separated by line-breaks, and event details by semicolon (;) as shown in the examples.
The first detail is the event time. It should always have both day and time of day separated by whitespace. For the day, you can use 
- a date, e.g. _2021-06-21_
- shortened weekday names, e.g. _mon_, _fri-sat_
- value _daily_ if the event occurs every day.

Event color can be specified in any CSS-accepted format (color name, hex, rgb, rgba, etc.). If you don't want to specify a color, always input a hyphen instead.

#### #protip: Host events.txt in [Dropbox](https://www.dropbox.com) for easy updating.

1. Place `events.txt` somewhere in your Dropbox.
2. Right-click it and select _Copy Dropbox Link_.
3. Edit `clocker.js` and locate line 3 `var events_txt = 'events.txt';`.
4. Replace `events.txt` with the Dropbox Link from your clipboard and save.

End result should look something like this:
```
var events_txt = 'https://www.dropbox.com/s/b666pwrytk1pepm/events.txt?dl=0';
```
