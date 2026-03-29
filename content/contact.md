---
title: "CONTACT"
type: "page"
layout: "single"
---

<div class="contact-layout">
  <div class="contact-details">
    <div class="contact-block">
      <h3>CHAMBER</h3>
      <p>Lawyers' Chamber No. 2, Above SBI<br>Punjab & Haryana High Court<br>Chandigarh</p>
    </div>
    <div class="contact-block">
      <h3>CHANDIGARH</h3>
      <p>#62, Sector 2<br>Chandigarh</p>
    </div>
    <div class="contact-block">
      <h3>MOHALI</h3>
      <p>#1608, Sector 60<br>Mohali</p>
    </div>
    <div class="contact-block">
      <h3>EMAIL</h3>
      <p><a href="mailto:contact@litigra.com">contact@litigra.com</a></p>
    </div>
  </div>

  <div class="contact-form-section">
    <h3 class="contact-form-heading">SEND A MESSAGE</h3>
    <form id="contact-form" class="contact-form">
      <div class="form-row">
        <div class="form-group">
          <label for="contact-name">Name</label>
          <input type="text" id="contact-name" name="name" required>
        </div>
        <div class="form-group">
          <label for="contact-email">Email</label>
          <input type="email" id="contact-email" name="email" required>
        </div>
      </div>
      <div class="form-group">
        <label for="contact-subject">Subject</label>
        <input type="text" id="contact-subject" name="subject">
      </div>
      <div class="form-group">
        <label for="contact-message">Message</label>
        <textarea id="contact-message" name="message" rows="5" required></textarea>
      </div>
      <button type="submit" class="btn btn-gold" id="contact-submit">Send Message</button>
      <div id="contact-status" class="contact-status"></div>
    </form>
  </div>
</div>

<script>
(function() {
  var form = document.getElementById('contact-form');
  var statusEl = document.getElementById('contact-status');
  var submitBtn = document.getElementById('contact-submit');

  form.addEventListener('submit', function(e) {
    e.preventDefault();
    submitBtn.disabled = true;
    submitBtn.textContent = 'Sending...';
    statusEl.className = 'contact-status';
    statusEl.textContent = '';

    var data = {
      name: document.getElementById('contact-name').value.trim(),
      email: document.getElementById('contact-email').value.trim(),
      subject: document.getElementById('contact-subject').value.trim(),
      message: document.getElementById('contact-message').value.trim()
    };

    fetch('https://litigra-contact.vaibhav-bb7.workers.dev', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(data)
    })
    .then(function(res) { return res.json(); })
    .then(function(result) {
      if (result.success) {
        statusEl.textContent = 'Your message has been sent. We will respond shortly.';
        statusEl.className = 'contact-status contact-status-success';
        form.reset();
      } else {
        statusEl.textContent = result.error || 'Something went wrong. Please try again.';
        statusEl.className = 'contact-status contact-status-error';
      }
      submitBtn.disabled = false;
      submitBtn.textContent = 'Send Message';
    })
    .catch(function() {
      statusEl.textContent = 'Could not send your message. Please email us directly.';
      statusEl.className = 'contact-status contact-status-error';
      submitBtn.disabled = false;
      submitBtn.textContent = 'Send Message';
    });
  });
})();
</script>
