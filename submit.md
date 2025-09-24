---
layout: default
title: Submit a story
---


<form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
<label>
Name (or “Anonymous”)
<input type="text" name="name" required>
</label>


<label>
Date of story
<input type="date" name="date" required>
</label>


<label>
Location (city, country)
<input type="text" name="location" required>
</label>


<p class="hint">If you know them, add coordinates (longitude, latitude). This helps us map it faster.</p>
<div style="display:grid; grid-template-columns:1fr 1fr; gap:.75rem">
<input type="text" name="lon" placeholder="Longitude (e.g. -3.1883)">
<input type="text" name="lat" placeholder="Latitude (e.g. 55.9533)">
</div>


<label>
Your story
<textarea name="story" rows="7" required></textarea>
</label>


<label>
Your email (optional, for follow-up)
<input type="email" name="email" placeholder="you@example.com">
</label>


<!-- Anti-spam honeypot -->
<input type="text" name="_gotcha" style="display:none">


<!-- Redirect after submit -->
<input type="hidden" name="_redirect" value="{{ '/thanks.html' | relative_url }}">


<button type="submit">Send</button>
</form>


<p class="hint">
By submitting, you consent to publication on our map. We may lightly edit for clarity.
</p>
