---
permalink: buddha.html
layout: default
title: "布袋和尚简介"
---
<div class="buddha">
  <div class="imgbuddha"><img src="/assets/img/Budai,_British_Museum.jpg" alt="布袋和尚，大英博物馆藏。" style="width: 100%;"><span style="font-size: 16px;">布袋和尚像</span></div>

  <div id="post">
    {% for post in site.posts %}
      {% if post.title == "「布袋和尚」东土应化事迹" %}
        {{ post.content }}
      {% endif %}
    {% endfor %}
  </div>
    
  {% unless site.posts.size == 1 %}
    <div style="text-align: center;">
      <button id="btn-prev" type="button" title="上一条">◀</button><button id="btn-next" type="button" title="下一条">▶</button><div id="loading" style="color: white; font-size: 85%; background-color: black; display: none;">加载中...</div>
    </div>
  {% endunless %}
</div>
<style>
  .buddha {
    font-family: simkai, kaiti, simsun, dengxian, simhei, serif;
    letter-spacing: -0.035em;
    max-width: 500px;
  }

  .imgbuddha {
    width: 120px;
  }

  .imgbuddha img {
    display: inherit;
  }

  button {
    display: inline-block;
    color: blue;
    background-color: transparent;
    border: 0;
    border-bottom: 1px dotted;
    cursor: pointer;
  }

  body.on-mobile .buddha {
    font-size: 16px;
    max-width: 100%;
  }

  body.on-mobile .imgbuddha {
    width: 40%;
  }
</style>
<script>
  document.querySelector('.brand').style.display = 'none';
</script>
<script>
  (function() {
    var btnPrev = document.getElementById('btn-prev');
    var btnNext = document.getElementById('btn-next');
    var post = document.getElementById('post');
    var loading = document.getElementById('loading');
    var postUrls = [];
    
    {% for post in site.posts %}
      postUrls.push("{{ post.url }}");
    {% endfor %}
    
    var postLength = postUrls.length;
    var currentPost = 0;
    var isFirstPost;
    var isLastPost;
    
    btnPrev.onclick = function(e) {
      e.preventDefault();
      
      isFirstPost = currentPost === 0;
      currentPost = isFirstPost ? (postLength - 1) : (currentPost - 1);
      
      request({
        method: 'GET',
        url: postUrls[currentPost]
      }, function() {
        loading.style.display = 'inline';
      },
      function(data) {
        post.innerHTML = data; 
        loading.style.display = 'none';
      });
    };

    btnNext.onclick = function(e) {
      e.preventDefault();
      
      isLastPost = currentPost === (postLength - 1);
      currentPost = isLastPost ?  0 : (currentPost + 1) ;
      
      request({
        method: 'GET',
        url: postUrls[currentPost]
      }, function() {
        loading.style.display = 'inline';
      },
      function(data) {
        post.innerHTML = data;
        loading.style.display = 'none';
      });
    };
  })();
</script>