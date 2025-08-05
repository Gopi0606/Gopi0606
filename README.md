<h1 align="center">Hi 👋, I'm Gopinath</h1>
<h3 align="center">I’m interested in Cyber Security</h3>

- 🌱 I’m currently learning **Ethical hacking**

- 📫 How to reach me **gopi661999@gmail.com**

<h3 align="left">Connect with me:</h3>
<p align="left">
<a href="https://linkedin.com/in/gopinath marimuthu" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="gopinath marimuthu" height="30" width="40" /></a>
</p>

<h3 align="left">Languages and Tools:</h3>
<p align="left"> <a href="https://www.gnu.org/software/bash/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/gnu_bash/gnu_bash-icon.svg" alt="bash" width="40" height="40"/> </a> <a href="https://www.cprogramming.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/c/c-original.svg" alt="c" width="40" height="40"/> </a> <a href="https://git-scm.com/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" alt="git" width="40" height="40"/> </a> <a href="https://www.w3.org/html/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" alt="html5" width="40" height="40"/> </a> <a href="https://www.linux.org/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/linux/linux-original.svg" alt="linux" width="40" height="40"/> </a> <a href="https://www.php.net" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/php/php-original.svg" alt="php" width="40" height="40"/> </a> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> </p>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub Snake Contributions</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            overflow: hidden; /* Prevent scrollbars due to canvas */
        }
        canvas {
            background-color: #ffffff;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            display: block;
            margin: auto; /* Center the canvas */
        }
    </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen p-4">
    <div class="bg-white p-6 rounded-xl shadow-lg max-w-4xl w-full text-center">
        <h1 class="text-3xl font-bold text-gray-800 mb-6">GitHub Contributions Snake</h1>
        <canvas id="contributionCanvas" class="w-full h-auto"></canvas>
        <p class="text-gray-600 mt-4">This visualization shows a year's worth of simulated GitHub contributions in a winding "snake" pattern. Darker squares indicate more contributions.</p>
    </div>

    <script>
        // Get the canvas element and its 2D rendering context
        const canvas = document.getElementById('contributionCanvas');
        const ctx = canvas.getContext('2d');

        // Define parameters for the contribution squares
        const squareSize = 10; // Size of each contribution square
        const spacing = 2;     // Spacing between squares
        const totalSize = squareSize + spacing; // Total space each square occupies

        // Define colors for different contribution levels (GitHub-like greens)
        const colors = [
            '#ebedf0', // No contributions (light grey)
            '#9be9a8', // Low contributions
            '#40c463', // Medium contributions
            '#30a14e', // High contributions
            '#216e39'  // Very high contributions
        ];

        // Function to generate dummy contribution data for a year
        function generateContributionData(days) {
            const data = [];
            let currentDate = new Date();
            currentDate.setDate(currentDate.getDate() - days); // Start from 'days' ago

            for (let i = 0; i < days; i++) {
                const count = Math.floor(Math.random() * 5); // Random count between 0 and 4
                data.push({
                    date: currentDate.toISOString().split('T')[0],
                    count: count
                });
                currentDate.setDate(currentDate.getDate() + 1);
            }
            return data;
        }

        // Generate 365 days of dummy contribution data
        const contributionData = generateContributionData(365);

        // Calculate canvas dimensions based on the data and desired layout
        const daysInRow = 52; // Approximately one year of weeks
        const numRows = Math.ceil(contributionData.length / daysInRow);

        let canvasWidth = daysInRow * totalSize + spacing;
        let canvasHeight = numRows * totalSize + spacing;

        // Set canvas dimensions
        canvas.width = canvasWidth;
        canvas.height = canvasHeight;

        // Function to draw a single contribution square
        function drawContributionSquare(x, y, count) {
            ctx.fillStyle = colors[count]; // Select color based on contribution count
            ctx.fillRect(x, y, squareSize, squareSize); // Draw the square
        }

        // Function to draw the entire snake contribution table
        function drawSnakeContributions() {
            ctx.clearRect(0, 0, canvas.width, canvas.height); // Clear the canvas

            for (let i = 0; i < contributionData.length; i++) {
                const day = contributionData[i];

                // Calculate row and column for the current day
                const row = Math.floor(i / daysInRow);
                let col = i % daysInRow;

                // Implement the "snake" pattern:
                // For even rows, draw left-to-right.
                // For odd rows, draw right-to-left.
                if (row % 2 !== 0) { // If it's an odd row
                    col = daysInRow - 1 - col; // Reverse the column order
                }

                // Calculate the x and y coordinates for the square
                const x = spacing + col * totalSize;
                const y = spacing + row * totalSize;

                // Draw the square
                drawContributionSquare(x, y, day.count);
            }
        }

        // Initial draw
        drawSnakeContributions();

        // Optional: Redraw on window resize for responsiveness
        window.addEventListener('resize', () => {
            // Recalculate dimensions if needed, or simply redraw if canvas size is fixed
            // For this specific visualization, the canvas size is fixed based on data,
            // but you might adjust it for more dynamic layouts.
            // For now, just redraw to ensure clarity if the browser resizes.
            drawSnakeContributions();
        });

        // You could add an animation loop here if you wanted the squares to appear one by one,
        // but for a static contributions table, a single draw is sufficient.
        // For example, to animate:
        // let currentDayIndex = 0;
        // function animateContributions() {
        //     if (currentDayIndex < contributionData.length) {
        //         const day = contributionData[currentDayIndex];
        //         const row = Math.floor(currentDayIndex / daysInRow);
        //         let col = currentDayIndex % daysInRow;
        //         if (row % 2 !== 0) {
        //             col = daysInRow - 1 - col;
        //         }
        //         const x = spacing + col * totalSize;
        //         const y = spacing + row * totalSize;
        //         drawContributionSquare(x, y, day.count);
        //         currentDayIndex++;
        //         requestAnimationFrame(animateContributions);
        //     }
        // }
        // animateContributions(); // Call to start animation
    </script>
</body>
</html>

