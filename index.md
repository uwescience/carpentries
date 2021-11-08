---
layout: landing      # DON'T CHANGE THIS.
# More detailed instructions (including how to fill these variables for an
# online workshop) are available at
# https://carpentries.github.io/workshop-template/customization/index.html
venue: "University of Washington"        # brief name of the institution that hosts the workshop without address (e.g., "Euphoric State University")
address: "online"      # full street address of workshop (e.g., "Room A, 123 Forth Street, Blimingen, Euphoria"), videoconferencing URL, or 'online'
country: "us"      # lowercase two-letter ISO country code such as "fr" (see https://en.wikipedia.org/wiki/ISO_3166-1#Current_codes) for the institution that hosts the workshop
language: "en"     # lowercase two-letter ISO language code such as "fr" (see https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) for the
latitude: "47.606209"        # decimal latitude of workshop venue (use https://www.latlong.net/)
longitude: "-122.332071"       # decimal longitude of the workshop venue (use https://www.latlong.net)
email: ["nben@uw.edu", "janekoh1@uw.edu"]    # boxed, comma-separated list of contact email addresses for the host, lead instructor, or whoever else is handling questions, like ["marlyn.wescoff@example.org", "fran.bilas@example.org", "ruth.lichterman@example.org"]
---

<div class="jumbotron">
  <div class="row">
    <div class="col-md-5">
      <img src="./assets/img/escience-logo.png" alt="Software Carpentries offered by the eScience Institute" title="Software Carpentries offered by the eScience Institute" style="width: 100%"/>
    </div>
    <div class="col-md-7">
      {% capture nowunix %}{{'now' | date: '%s'}}{% endcapture %}
      {% assign sorted = site.pages | sort: 'startdate' | reverse %}

      {% assign upcoming = '' | split: '' %}
      {% assign past = '' | split: '' %}
      {% for page in sorted %}
        {% capture posttime %}{{page.startdate | date: '%s'}}{% endcapture %}
        {% if page.layout == 'workshop' %}
          {% if posttime >= nowunix  %}
            {% assign upcoming = upcoming | push: page %}
          {% else %}  
            {% assign past = past | push: page %}
          {% endif %}
        {% endif %}
      {% endfor %}

      {% if upcoming.size > 1 or upcoming.size == 0%}
        <h2 id="next_event">Upcoming workshops</h2>
      {% else %}
        <h2 id="next_event">Upcoming workshop</h2>
      {% endif %}

      {% if upcoming.size >= 1 %}
        <ul>
          {% for page in upcoming %}
            <li>
              <a href=".{{ page.url }}">{{ page.humandate }} ({{ page.address }})</a>
            </li>
          {% endfor %}
        </ul>
      {% else %}
        <i>The next workshop is yet to be scheduled. Stay tuned!</i>
      {% endif %}

      <h2 id="next_event">Get notified</h2>
      Sign up for the <a href="https://mailman11.u.washington.edu/mailman/listinfo/escience_education">eScience Education Working Group mailing list</a> to get notified when the next workshop registration opens:
      <form style="margin-top: 1em" action="https://mailman11.u.washington.edu/mailman/subscribe/escience_education" method="POST">
      E-mail: <input name="email" />&nbsp;<input type="submit" value="Sign Me Up!" />
      <input type=radio name="digest" value="0" CHECKED style="display: none">
      </form>
    </div>
  </div>
</div>

<h2 id="general">General Information</h2>

{% comment %}
INTRODUCTION

Edit the general explanatory paragraph below if you want to change
the pitch.
{% endcomment %}
{% if site.carpentry == "swc" %}
{% include swc/intro.html %}
{% elsif site.carpentry == "dc" %}
{% include dc/intro.html %}
{% elsif site.carpentry == "lc" %}
{% include lc/intro.html %}
{% endif %}

{% if site.pilot %}
This is a pilot workshop, testing out a lesson that is still under development. The lesson authors would appreciate any feedback you can give them about the lesson content and suggestions for how it could be further improved.
{% endif %}

{% comment %}
AUDIENCE

Explain who your audience is.  (In particular, tell readers if the
workshop is only open to people from a particular institution.
{% endcomment %}
{% if site.carpentry == "swc" %}
{% include swc/who.html %}
{% elsif site.carpentry == "dc" %}
{% include dc/who.html %}
{% elsif site.carpentry == "lc" %}
{% include lc/who.html %}
{% endif %}

{% comment %}
SPECIAL REQUIREMENTS

Modify the block below if there are any special requirements.
{% endcomment %}
<p id="requirements">
  <strong>Requirements:</strong>
  {% if online == "false" %}
    Participants must bring a laptop with a
    Mac, Linux, or Windows operating system (not a tablet, Chromebook, etc.) that they have administrative privileges on.
  {% else %}
    Participants must have access to a computer with a
    Mac, Linux, or Windows operating system (not a tablet, Chromebook, etc.) that they have administrative privileges on.
  {% endif %}
  Each workshop may request a few specific software packages be installed in advance. Participants can check the page of the workshop they'll be attending for specific setup instructions.
</p>

{% comment %}
ACCESSIBILITY

Modify the block below if there are any barriers to accessibility or
special instructions.
{% endcomment %}
<p id="accessibility">
  <strong>Accessibility:</strong>
{% if online == "false" %}
  We are committed to making this workshop
  accessible to everybody.  For workshops at a physical location, the workshop organizers have checked that:
</p>
<ul>
  <li>The room is wheelchair / scooter accessible.</li>
  <li>Accessible restrooms are available.</li>
</ul>
<p>
  Materials will be provided in advance of the workshop and
  large-print handouts are available if needed by notifying the
  organizers in advance.  If we can help making learning easier for
  you (e.g. sign-language interpreters, lactation facilities) please
  get in touch (using contact details below) and we will
  attempt to provide them.
</p>
{% else %}
  We are dedicated to providing a positive and accessible learning environment for all. Please
  notify the instructors in advance of the workshop if you require any accommodations or if there is
  anything we can do to make this workshop more accessible to you.
</p>
{% endif %}

{% comment %}
CONTACT EMAIL ADDRESS

Display the contact email address set in the configuration file.
{% endcomment %}
<p id="contact">
  <strong>Contact:</strong>
  Please email
  {% if page.email %}
  {% for email in page.email %}
  {% if forloop.last and page.email.size > 1 %}
  or
  {% else %}
  {% unless forloop.first %}
  ,
  {% endunless %}
  {% endif %}
  <a href='mailto:{{email}}'>{{email}}</a>
  {% endfor %}
  {% else %}
  to-be-announced
  {% endif %}
  for more information.
</p>

<p id="roles">
  <strong>Roles:</strong>
  To learn more about the roles at the workshop (who will be doing what),
  refer to <a href="https://carpentries.org/workshop_faq/#what-are-the-roles-of-everyone-participating-in-a-workshop">our Workshop FAQ</a>.
</p>

{% comment %}
WHO CAN ATTEND?

If you would like to specify who can attend the workshop,
you can use the section below.

Move the 'endcomment' tag above the beginning of the following
<p> tag to make this section visible.

Edit the text to match who can attend the workshop. For instance:
- This workshop is open to affiliates to ABC university.
- This workshop is open to the public.
- If you are interested in attending this workshop, contact me@example.com
  for more information

<p id="who-can-attend">
    <strong>Who can attend?:</strong>
    This workshop is open to ....
</p>
{% endcomment %}

<hr/>

<h2 id="past_events">Previous workshops</h2>

<ul>
  {% for page in past %}
    <li>
      <a href=".{{ page.url }}">{{ page.humandate }} ({{ page.address }})</a>
    </li>
  {% endfor %}
</ul>

<hr/>

{% comment%}
CODE OF CONDUCT
{% endcomment %}
<h2 id="code-of-conduct">Code of Conduct</h2>

<p>
Everyone who participates in Carpentries activities is required to conform to the <a href="https://docs.carpentries.org/topic_folders/policies/code-of-conduct.html">Code of Conduct</a>. This document also outlines how to report an incident if needed.
</p>

<p class="text-center">
  <a href="https://goo.gl/forms/KoUfO53Za3apOuOK2">
    <button type="button" class="btn btn-info">Report a Code of Conduct Incident</button>
  </a>
</p>

