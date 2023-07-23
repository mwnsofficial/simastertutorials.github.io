---
title: Kontak
layout: default
description: menghubungkan ke Simaster
permalink: "/contact.html"
---
<!-- page title -->
<section class="page-title-section overlay" data-background="images/backgrounds/page-title.jpg">
  <div class="container">
    <div class="row">
      <div class="col-md-8">
        <ul class="list-inline custom-breadcrumb mb-2">
          <li class="list-inline-item"><a class="h2 text-primary font-secondary" href="index.html">Beranda</a></li>
          <li class="list-inline-item text-white h3 font-secondary nasted">{{page.title}}</li>
        </ul>
        <p class="text-lighten mb-0">{{page.description}}.</p>
      </div>
    </div>
  </div>
</section>
<!-- /page title -->

<!-- contact -->
<section class="section bg-gray">
  <div class="container">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="section-title">{{page.title}}</h2>
      </div>
    </div>
    <div class="row">
      <div class="col-lg-7 mb-4 mb-lg-0">
        <form action="mailto:myarachma92@gmail.com" method="POST">
          <input type="text" class="form-control mb-3" id="name" name="name" placeholder="Your Name" required>
          <input type="email" class="form-control mb-3" id="mail" name="mail" placeholder="Your Email" required>
          <input type="text" class="form-control mb-3" id="subject" name="subject" placeholder="Subject" required>
          <textarea name="message" id="message" class="form-control mb-3" placeholder="Your Message" required></textarea>
          <button type="submit" value="send" class="btn btn-primary">SEND MESSAGE</button>
        </form>
      </div>
      <div class="col-lg-5">
        <p class="mb-5">Simaster Tutorials akan selalu terbuka untuk terhubung dengan siapa pun untuk mempermudah interaktif dan komunikatif</p>
        <a href="tel:+6287764241047" class="text-color h5 d-block">+62 877 6424 1047</a>
        <a href="mailto:myarachma92@email.com" class="mb-5 text-color h5 d-block">myarachma92@gmail.com</a>
        <p>Kec. Gambut, Kab. Banjar<br>INDONESIA</p>
      </div>
    </div>
  </div>
</section>
<!-- /contact -->

<!-- gmap -->
<section class="section pt-0">
  <!-- Google Map -->
  <div id="map_canvas" data-latitude="-3,4081566" data-longitude="114,6711959"></div>
</section>
<!-- /gmap -->
