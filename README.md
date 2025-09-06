# Photo-protal
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Shree Ganesh Creation - Photo Upload Portal</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/croppie/2.6.5/croppie.min.css" />
  <style>
    body { font-family: Arial, sans-serif; text-align: center; }
    .grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 10px; margin: 20px; }
    .slot { width: 150px; height: 100px; border: 2px dashed #999; display: flex; align-items: center; justify-content: center; cursor: pointer; }
    .slot img { max-width: 100%; max-height: 100%; }
    input, button { margin: 10px; padding: 10px; font-size: 16px; }
  </style>
</head>
<body>

  <h1>📸 Shree Ganesh Creation</h1>
  <h3>Upload & Adjust Your Photos</h3>

  <label>Choose Layout: </label>
  <select id="layout" onchange="generateGrid()">
    <option value="13">13 Photos</option>
    <option value="17">17 Photos</option>
    <option value="21">21 Photos</option>
  </select>

  <div id="gridContainer" class="grid"></div>

  <input type="text" id="orderId" placeholder="Enter Order ID" required>
  <br>
  <button onclick="submitOrder()">✅ Done</button>

  <script>
    function generateGrid() {
      let grid = document.getElementById("gridContainer");
      grid.innerHTML = "";
      let count = document.getElementById("layout").value;
      for (let i = 0; i < count; i++) {
        let div = document.createElement("div");
        div.className = "slot";
        div.innerHTML = "Click to Upload";
        div.onclick = () => uploadPhoto(div);
        grid.appendChild(div);
      }
    }

    function uploadPhoto(div) {
      let input = document.createElement("input");
      input.type = "file";
      input.accept = "image/*";
      input.onchange = e => {
        let file = e.target.files[0];
        let reader = new FileReader();
        reader.onload = () => {
          div.innerHTML = `<img src="${reader.result}" />`;
        }
        reader.readAsDataURL(file);
      }
      input.click();
    }

    function submitOrder() {
      let orderId = document.getElementById("orderId").value;
      if (!orderId) {
        alert("⚠️ Please enter Order ID!");
        return;
      }
      alert("✅ Order Submitted! Order ID: " + orderId + "\nPhotos will be sent to server.");
      // यहां backend code (PHP/Node.js/Firebase) लगेगा ताकि data save हो सके
    }

    // Default grid load
    generateGrid();
  </script>
</body>
</html>
