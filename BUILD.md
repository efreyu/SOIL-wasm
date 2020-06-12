#### Docker configuration for emscripten debugging
The assembly provides 2 containers, ubuntu for assembly and nginx for the web server

#### Installing 

***First setup***
1. Clone repository
2. Set run.sh executable `chmod +x run.sh`
3. Run containers

***Desktop build***
```bash
mkdir build && cd build
cmake ..
make
```

***Wasm build in container***
```bash
./run.sh --run
./run.sh --wasm-build
```

After running just visit `https://localhost:8080/`

####Command list
```bash
chmod +x game.sh
./game.sh -b                    # Build all containers
./game.sh -r                    # Run all containers
./game.sh --wasm-build          # Project compilation
./game.sh --test                # Run tests
./game.sh -o ubuntu bash [cmd]  # Execute an arbitrary command in the container
./game.sh -d                    # To stop containers
./game.sh --help                # to get help
```