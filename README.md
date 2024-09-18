# shopify-redirect
Show a popup to US visitors to your Shopify store and give them button options to be redirected, or continue shopping on the Canadian website.

Obviously this will work with any Country code, you just need to Google for specific country codes. For example, if it was Australia in your situation, you'd use AU instead of US, etc etc...

Copy and paste this code (including the script tag) directly into theme.liquid, at the bottom just before a closing body tag like this

<script>
  document.addEventListener('DOMContentLoaded', function() {
    
    function showPopup() {
      const popup = document.createElement('div');
      popup.innerHTML = `
        <div class="popup-overlay">
          <div class="popup-content">
            <img width="12000" src="{{ 'united-states.png' | asset_url }}" alt="US Flag" class="popup-flag" />
            <h1>Shopping from the USA?  Click "Redirect me" to shop from our US store.</h1>
            <button class="popup-button" onclick="window.location.href='https://www.chem-x.com/?ref=LargeCar'">Yes, redirect me</button>
            <button class="popup-button" onclick="this.parentElement.parentElement.remove()">No, stay here</button>
          </div>
        </div>
      `;
      document.body.appendChild(popup);
      
      localStorage.setItem('popupShown', 'true');
    }

    
    if (localStorage.getItem('popupShown') !== 'true') {
      // Use Shopify's global variables to determine the visitor's country
      if (window.Shopify && window.Shopify.country) {
        const countryCode = window.Shopify.country;
    console.log('countryCode: ', countryCode)
        if (countryCode === 'US') {
          showPopup();
        }
      } else {
        console.error('Shopify global variables not available');
      }
    }
  });
</script>
</body>
</html>
