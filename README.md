# toro

<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome Gyro</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
        h1 {
            margin-top: 20px;
        }
        button {
            margin: 10px;
            padding: 10px 20px;
            font-size: 16px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        p {
            font-size: 20px;
        }
    </style>
</head>
<body>
    <h1>Gyroscope Values</h1>
    <div>
        <button id="gyroButton">Start Gyroscope</button>
    </div>
    <div id="gyro-values" style="display: none;">
        <p>X Axis: <span id="x-axis"></span></p>
        <p>Y Axis: <span id="y-axis"></span></p>
        <p>Z Axis: <span id="z-axis"></span></p>
    </div>

    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>
    $(document).ready(function() {
        var gyroButton = document.getElementById("gyroButton");
        var xAxisValue = document.getElementById("x-axis");
        var yAxisValue = document.getElementById("y-axis");
        var zAxisValue = document.getElementById("z-axis");

        function handleOrientation(event) {
            var x = event.beta; // X 軸的傾斜角度 (-180 到 180 度)
            var y = event.gamma; // Y 軸的傾斜角度 (-90 到 90 度)
            var z = event.alpha; // Z 軸的方向角度 (0 到 360 度)

            xAxisValue.textContent = x.toFixed(2);
            yAxisValue.textContent = y.toFixed(2);
            zAxisValue.textContent = z.toFixed(2);
        }

        $('#gyroButton').on('click', function() {
            if (typeof DeviceOrientationEvent.requestPermission === 'function') {
                DeviceOrientationEvent.requestPermission()
                    .then(permissionState => {
                        if (permissionState === 'granted') {
                            // 顯示陀螺儀數據區塊
                            $('#gyro-values').css('display', 'block');
                            // 開始監聽陀螺儀數據
                            window.addEventListener("deviceorientation", handleOrientation, true);
                        } else {
                            alert("Permission denied to access gyroscope.");
                        }
                    })
                    .catch((err) => {
                        console.log(err);
                    });
            } else {
                alert("Device orientation not supported.");
            }
        });
    });
</script>
</body>
</html>
