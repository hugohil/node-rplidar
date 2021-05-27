# node-rplidar
A Node module to communicate with the RPLidar over USB.

This fork is a temporary fix for issues on Raspberry Pi with [switching `dtr` flag](https://github.com/serialport/node-serialport/issues/2240). It simply uses version `8.0.8` of `serialport` instead of `9.0.7`.

## installation
```
npm install git+https://git@github.com/hugohil/node-rplidar.git
```

## usage
Always make sure to call lidar.health before starting a new scan.
```javascript
const RPLidar = require('node-rplidar');
const lidar = RPLidar('/dev/ttyUSB0');

lidar.on('data', (data) => {
  console.log(data);
});

lidar
  .init()
  .then(lidar.health)
  .then((health) => {
    console.log('health', health);

    // 0 = good, 1 = warning, 2 = error
    if (health.status === 0) {
      lidar.scan();
    }
  });
```
