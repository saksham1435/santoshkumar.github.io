<html lang="en">
<head></head>
<body>﻿

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, 

initial-scale=1.0">
    <title>YouTube Video Points Tracker</title>
    <style>
        /* Reset some default browser styling */
        body, h1, p {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Roboto', sans-serif;
            background: linear-gradient(to right, #6a11cb, 

#2575fc);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .container {
            max-width: 90%;
            width: 360px;
            background-color: #ffffff;
            border-radius: 12px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            padding: 20px;
            text-align: center;
        }

        h1 {
            font-size: 1.8em;
            color: #333;
            margin-bottom: 20px;
            font-weight: 700;
        }

        .video-container {
            margin-bottom: 20px;
        }

        iframe {
            width: 100%;
            height: 200px; /* Adjust height for better mobile 

view */
            border: none;
            border-radius: 8px;
            background-color: #000;
        }

        .points-container {
            font-size: 1.6em;
            margin-top: 20px;
            color: #333;
            font-weight: 700;
        }

        button {
            background-color: #2575fc;
            color: #ffffff;
            border: none;
            border-radius: 8px;
            padding: 10px 20px;
            font-size: 1em;
            cursor: pointer;
            transition: background-color 0.3s;
            margin-top: 20px;
        }

        button:hover {
            background-color: #1d4ed8;
        }

        @media (min-width: 768px) {
            .container {
                width: 600px; /* Wider container on larger 

screens */
            }

            iframe {
                height: 315px; /* Standard height for larger 

screens */
            }

            h1 {
                font-size: 2.2em; /* Larger heading for 

larger screens */
            }

            .points-container {
                font-size: 2em; /* Larger font size for 

points on larger screens */
            }
        }
    </style>
<script defer="" data-

domain="2artistsantoshkumarpatil.tiiny.site" 

src="https://analytics.tiiny.site/js/plausible.js"></script><

script type="text/javascript" src="https://tiiny.host/ad-

script.js"></script>

    <div class="container">
        <h1>YouTube Video Points Tracker</h1>
        <div id="video-container" class="video-container">
            <!-- The iframe will be inserted by JavaScript 

-->
        </div>
        <div class="points-container">
            <p>Points: <span id="points">0</span></p>
        </div>
        <button id="shareScoreButton">Share Your 

Score</button>
    </div>
    <script 

src="https://www.youtube.com/iframe_api"></script>
    <script>
        let points = 0;
        let lastUpdateTime = Date.now();
        let isPaused = false;
        let player;
        let videoIds = [
            'A0eWyzNteuQ', 'pfEv6gCrkbM', 'Ngs2xko0q50', 

'r0dkm_yc3WI', 'y_SoTEm9CpQ',
            '9EXY-zJ5KoU', 'o9WD0U4gZ1U', 'yYqIgr0IVkk', 

'4jgt94NrOHM', 'jAmgUg2-Xow',
            'WozQFoSWZUI', 'lXoDMRYGAbE', 'EMHjVxvhjsY', 

'H--76wmHtQg', 'DbqhRS1LJag',
            'djps3dEn5uA', 'vAb1lBVn-7o', 'R1aSwh0SZic', 

'6hZqZuqyl40', 'SHHvxT-xkuw',
            'wLugHfkDxGA', 'T1tVvhlkJwQ', 'Mzw-2dbmXJg', 

'jZ0Z_WySgMA', 'rVVAEmmwIvE',
            'nZ77qKia50w', '1sqxrIITEFI', '-QgG0XSTAS8', 

'P8p22_CBqcw', 'W8CAGSEJ-Kk',
            'phaH9SYI1MM', 'xHSvoT5MHQA', 'jgYN-Bh7qIc', 

'XYV0VBfRAC8', '5jwTq3-eNHs',
            'QRtLtIyWH3E', 'GhXoSWLdbzY', 'hnpqmCepXZg', 

'WCcrGmyJKwE', 'hIvInjjMaTg',
            '4NkolG3AxTI', 'cMzg2qtaPVQ', 'hJPoex2w-sI', 

'XutGQrU6u-c', 'GWxUK5ZnCPs',
            'ebPFVvb0VHE', '_rraZxemWKA', 'Tb8qrkQL1j0', 

'AdqfdsXE3a8', '-YEhusdGYzw',
            'y67hfUaTLh8', 'R2nStWZClDw', 'rh9p3YKf8OI', 

'fukWf3Y00vg', 'ZrMhNeZOpVo',
            'COG63YJS5y0', '73YTyjtDGqg', 'hjHMHHh3_YM', 

'W9MvaLckvtM', '-y7_kSEUJis',
            '_VCky__Eujk', '8Clpt58rq4s', 'i556vhi69Y4', 

'uYUlDk1TKY8', 'F0NV540ipfs',
            '7B-CVfZT5qE', 'l2Mm15Adk_Q', '-Qdj-VLG-ss', 

'dZoqn16mPe0', 'iqSRi_UF8lA',
            'C_Ctr92YDRE', 'Vkhe0xOzBxE', 'IG9lHQB6o4Y', 

'OO5lptna__I', '98FGX-QZ8zw',
            'n6_wEIpmvpk', 'iH7OGogeD_I', '4S7bIIFcmXc', 

'yr83_9N6_pI', 'lTHzX9DR6Nc',
            'LL7CpagWiPs', 'cawHCaRuYQw', 'dY09ylRxZW0', 

'Rh_flSTDtKI', 'e0A1p_0IxhM',
            'eo0Jk7uCj1s', '6gSNLqf4S3k', 'MyBaZZUXnUU', 

'rq9e-hpjzbw', 'i11YA-R3AJQ',
            '7Y6kglyd33I', 'YRVpRACWx5Q', 'ZZzJZ_-1PRk', 

'SdOR7W4tD-c', 'HZUyYHXbSIk',
            'ImujXS3mOxU', 'JUw-1ttwq9E', 'EidHfyF9peM', 

'd59oXDUQqzU', 'Qhnbn1mx68A',
            'MdQZp04up-0', 'nI8qMNQYA10', 'RQ346iqknao', 

'cn6bhIObUDs', 'EnNbItTZdtY',
            'ylX_uFZz0Ok', 'wPj2PVdlfC0', 'tlR0hy2FPK0', 

'hzw95E1sBAM', 'qUjdUgfmKyk'
        ];
        let currentVideoIndex = 0;
        let lastPlaybackPosition = 0;
        let shuffledVideoIds = [];

        function onYouTubeIframeAPIReady() {
            const userId = getUniqueId(); // Get or generate 

unique user ID
            shuffledVideoIds = getShuffledVideoIds(userId); 

// Get shuffled video order
            lastPlaybackPosition = getPlaybackPosition(); // 

Get saved playback position
            currentVideoIndex = getCurrentVideoIndex(); // 

Get saved video index
            loadPlayer();
        }

        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 

1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        function getShuffledVideoIds(userId) {
            let shuffledIds = localStorage.getItem

("shuffledVideoIds");
            if (!shuffledIds) {
                shuffledIds = shuffleArray([...videoIds]);
                localStorage.setItem("shuffledVideoIds", 

JSON.stringify(shuffledIds));
            } else {
                shuffledIds = JSON.parse(shuffledIds);
            }
            return shuffledIds;
        }

        function loadPlayer() {
            const videoId = shuffledVideoIds

[currentVideoIndex];
            if (player) {
                player.loadVideoById(videoId);
            } else {
                player = new YT.Player("video-container", {
                    videoId: videoId,
                    events: {
                        onStateChange: onPlayerStateChange
                    }
                });
            }
        }

        function updatePoints() {
            const playbackPosition = player.getCurrentTime();
            const playbackDuration = playbackPosition - 

lastPlaybackPosition;
            if (playbackDuration >= 10) {
                points += 10;
                document.getElementById("points").textContent 

= points;
                lastPlaybackPosition = playbackPosition;
                localStorage.setItem("points", points); // 

Save points in local storage
                savePlaybackPosition(playbackPosition);
            }
        }

        function savePlaybackPosition(position) {
            localStorage.setItem("playbackPosition", 

position);
        }

        function getPlaybackPosition() {
            return parseFloat(localStorage.getItem

("playbackPosition")) || 0;
        }

        function getCurrentVideoIndex() {
            return parseInt(localStorage.getItem

("currentVideoIndex")) || 0;
        }

        function onPlayerStateChange(event) {
            if (event.data === YT.PlayerState.PLAYING) {
                isPaused = false;
                const elapsedTime = Date.now() - 

lastUpdateTime;
                if (elapsedTime >= 10000) {
                    updatePoints();
                    lastUpdateTime = Date.now();
                }
            } else if (event.data === YT.PlayerState.PAUSED) 

{
                isPaused = true;
            } else if (event.data === YT.PlayerState.ENDED) {
                currentVideoIndex++;
                if (currentVideoIndex >= 

shuffledVideoIds.length) {
                    currentVideoIndex = 0; // Restart from 

the beginning
                }
                loadPlayer();
            }
        }

        function getUniqueId() {
            let uniqueId = localStorage.getItem("uniqueId");
            if (!uniqueId) {
                uniqueId = Math.random().toString

(36).substring(2, 15);
                localStorage.setItem("uniqueId", uniqueId);
            }
            return uniqueId;
        }

        document.getElementById

("shareScoreButton").addEventListener("click", function() {
            const shareText = `I scored ${points} points 

watching videos! 🎉`;
            if (navigator.share) {
                navigator.share({
                    title: "YouTube Video Points Tracker",
                    text: shareText,
                    url: window.location.href
                }).catch(console.error);
            } else {
                prompt("Copy and share your score:", 

shareText);
            }
        });
    </script>

</body>
</html>
      
