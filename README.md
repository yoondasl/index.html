<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Canvas Creative Flower</title>
</head>
<body>
    <canvas id="flowerCanvas" width="800" height="800"></canvas>
    <script>
        const canvas = document.getElementById('flowerCanvas');
        const ctx = canvas.getContext('2d');

        const petalColors = ['#FF69B4', '#FF1493', '#C71585', '#DB7093', '#FFC0CB'];

        function getRandomColor() {
            return petalColors[Math.floor(Math.random() * petalColors.length)];
        }

        function drawPetal(cx, cy, rx, ry, angle) {
            ctx.save();
            ctx.translate(cx, cy);
            ctx.rotate(angle);
            ctx.beginPath();
            ctx.moveTo(0, 0);
            ctx.quadraticCurveTo(rx / 1, -ry, rx, 0);
            ctx.quadraticCurveTo(rx / 2, ry, 0, 0);
            ctx.fillStyle = getRandomColor(); // 랜덤한 색상 선택
            ctx.fill();
            ctx.restore();
        }

        function drawFlower(centerX, centerY) {
            const petalRadiusX = 35;
            const petalRadiusY = 80;
            const petalCount = 10;
            const angleStep = (2 * Math.PI) / petalCount;

            for (let i = 0; i < petalCount; i++) {
                const angle = i * angleStep;
                drawPetal(centerX, centerY, petalRadiusX, petalRadiusY, angle);
            }

            // Draw center
            ctx.beginPath();
            ctx.arc(centerX, centerY, 20, 0, Math.PI * 2);
            ctx.fillStyle = 'yellow';
            ctx.fill();
            ctx.closePath();
        }

        function drawMultipleFlowers(rows, cols, spacing) {
            const startX = spacing / 2;
            const startY = spacing / 2;
            for (let row = 0; row < rows; row++) {
                for (let col = 0; col < cols; col++) {
                    const x = startX + col * spacing;
                    const y = startY + row * spacing;
                    drawFlower(x, y);
                    console.log(`Drawing flower at (${x}, ${y})`);
                }
            }
        }

        drawMultipleFlowers(5, 5, 100); // 간격을 150으로 변경
    </script>
</body>
</html>
