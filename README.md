<!doctype html>
<html lang="id"> 
 <head> 
  <meta charset="UTF-8"> 
  <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
  <title>Sistem Rating dan Ulasan</title> 
  <style>
        body { font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto; padding: 20px; }
        .star { color: #ddd; font-size: 30px; cursor: pointer; }
        .star.active { color: #ffd700; }
        textarea { width: 100%; height: 100px; margin-bottom: 10px; }
        button { background-color: #4CAF50; color: white; padding: 10px 20px; border: none; cursor: pointer; }
        #reviews { margin-top: 20px; }
        .review { border-bottom: 1px solid #ddd; padding: 10px 0; }
    </style> 
 </head> 
 <body> 
  <h1>Beri Rating dan Ulasan</h1> 
  <div id="stars"> <span class="star" data-value="1">★</span> <span class="star" data-value="2">★</span> <span class="star" data-value="3">★</span> <span class="star" data-value="4">★</span> <span class="star" data-value="5">★</span> 
  </div> 
  <p>Rating Anda: <span id="rating">0</span> dari 5</p> <textarea id="review" placeholder="Tulis ulasan Anda di sini..."></textarea> <button onclick="submitReview()">Kirim Ulasan</button> 
  <div id="reviews"></div> 
  <script>
        const stars = document.querySelectorAll('.star');
        const ratingDisplay = document.getElementById('rating');
        let currentRating = 0;

        stars.forEach(star => {
            star.addEventListener('mouseover', selectStars);
            star.addEventListener('mouseout', unselectStars);
            star.addEventListener('click', setRating);
        });

        function selectStars(e) {
            const value = e.target.dataset.value;
            stars.forEach(star => {
                star.classList.toggle('active', star.dataset.value <= value);
            });
        }

        function unselectStars() {
            stars.forEach(star => {
                star.classList.toggle('active', star.dataset.value <= currentRating);
            });
        }

        function setRating(e) {
            currentRating = e.target.dataset.value;
            ratingDisplay.textContent = currentRating;
            unselectStars();
        }

        function submitReview() {
            const reviewText = document.getElementById('review').value;
            if (currentRating === 0) {
                alert('Mohon beri rating terlebih dahulu!');
                return;
            }
            if (reviewText.trim() === '') {
                alert('Mohon tulis ulasan Anda!');
                return;
            }

            const reviewsContainer = document.getElementById('reviews');
            const reviewElement = document.createElement('div');
            reviewElement.className = 'review';
            reviewElement.innerHTML = `
                <p><strong>Rating:</strong> ${currentRating}/5</p>
                <p><strong>Ulasan:</strong> ${reviewText}</p>
            `;
            reviewsContainer.prepend(reviewElement);

            // Reset form
            currentRating = 0;
            ratingDisplay.textContent = '0';
            document.getElementById('review').value = '';
            unselectStars();

            alert('Terima kasih atas ulasan Anda!');
        }
    </script> 
 </body>
</html>
