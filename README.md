# Egg-opener-2
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Egg Opener Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f7f7f7;
            padding: 20px;
        }
        .button {
            padding: 15px 25px;
            font-size: 20px;
            color: #fff;
            background-color: #007BFF;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .button:hover {
            background-color: #0056b3;
        }
        .output {
            margin-top: 20px;
            font-size: 24px;
            color: #333;
            opacity: 0;
            animation: fadeIn 0.5s forwards;
        }
        /* Animation for the pet result */
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: scale(0.8);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }
        /* Style for the pet name popup */
        .pet-popup {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            border: 2px solid #ccc;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            opacity: 0;
            animation: fadeInScale 0.7s forwards;
        }
        @keyframes fadeInScale {
            from {
                opacity: 0;
                transform: translate(-50%, -50%) scale(0.8);
            }
            to {
                opacity: 1;
                transform: translate(-50%, -50%) scale(1);
            }
        }
    </style>
</head>
<body>
    <h1>Egg Opener Simulator</h1>
    <button class="button" onclick="openEgg()">Open Egg</button>
    <div class="output" id="output">Click the button to open an egg!</div>
    <div id="popupContainer"></div>

    <script>
        // Pets and their probabilities
        const pets = [
            { name: "Common Cat", chance: 60.0 },
            { name: "Common Dog", chance: 20.0 },
            { name: "Uncommon Bird", chance: 10.0 },
            { name: "Rare Fox", chance: 5.0 },
            { name: "Epic Dragon", chance: 2.5 },
            { name: "Legendary Unicorn", chance: 1.0 },
            { name: "Mythic Phoenix", chance: 0.5 },
            { name: "Divine Tiger", chance: 0.25 },
            { name: "Godly Wolf", chance: 0.1 },
            { name: "Celestial Whale", chance: 0.05 },
            { name: "Stellar Griffin", chance: 0.02 },
            { name: "Galactic Serpent", chance: 0.01 },
            { name: "Astral Beast", chance: 0.005 },
            { name: "Ethereal Spirit", chance: 0.001 },
            { name: "Ultimate Egglord", chance: 0.00001 },
        ];

        // Calculate total chance
        const totalChance = pets.reduce((sum, pet) => sum + pet.chance, 0);

        // Function to draw a random pet
        function openEgg() {
            const random = Math.random() * totalChance;
            let cumulativeChance = 0;

            for (const pet of pets) {
                cumulativeChance += pet.chance;
                if (random <= cumulativeChance) {
                    showPopup(pet.name);
                    return;
                }
            }

            showPopup("No pet found (this shouldn't happen!)");
        }

        // Function to display popup with animation
        function showPopup(petName) {
            const popupContainer = document.getElementById("popupContainer");

            // Clear previous popup
            popupContainer.innerHTML = "";

            // Create popup element
            const popup = document.createElement("div");
            popup.className = "pet-popup";
            popup.textContent = `You got: ${petName}`;

            // Add popup to container
            popupContainer.appendChild(popup);

            // Remove popup after 3 seconds
            setTimeout(() => {
                popup.remove();
            }, 3000);
        }
    </script>
</body>
</html>
