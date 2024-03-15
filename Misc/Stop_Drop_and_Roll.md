<h1>Solution: Stop Drop and Roll</h1>

<h3>This challenge hwo a room that made you basically do a simon says type of game.</h3>

Here is the rules that it shows you when you start the NC connection.

<img src="https://i.imgur.com/aQLyyPK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

I actually made a script for the challenge and did goe through every prompt like I did for the character challenege LOL. 
The script has two functions respond to scenario and handle netcat connection.

```python3
import socket

def respond_to_scenario(scenarios): # handles each prompt by taking a list and then creates a string of the responses
    response_map = {
        'GORGE': 'STOP',
        'PHREAK': 'DROP',
        'FIRE': 'ROLL'
    }
    scenario_list = scenarios.split(',')
    responses = [response_map.get(scenario.strip().upper(), 'UNKNOWN') for scenario in scenario_list]
    return '-'.join(responses)

def handle_netcat_connection(host, port): # this connects to the box while sending the responses from the priviouse function
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((host, port))
        print(f"Connected to {host}:{port}")
        started = False
        
        try:
            while True:
                data = s.recv(1024).decode().strip()

                # checks for the are you ready and repsonds with y
                if "Are you ready? (y/n)" in data:
                    print("Received: Are you ready? (y/n)")
                    s.sendall(b"y\n")
                    print("Sending response: y")
                    started = True
                    continue

                if data == "What do you do?": # this ignores the what od you do for each prompt
                    continue

                # Once started, process scenarios
                if started:
                    # Process each received message after the game has started
                    print(f"Received: {data}")
                    # Check for 'What do you do?' at the end and remove it
                    if data.endswith("What do you do?"):
                        data = data[:-len("What do you do?")].strip()
                    #check for ok lets go when challenge starts
                    if data.startswith("Ok then! Let's go!"):
                        data = data[len("Ok then! Let's go!"):].strip()
                    #this respondes to each prompt with the responses from the respond to scenario function
                    response = respond_to_scenario(data)
                    print(f"Sending response: {response}")
                    s.sendall(response.encode() + b'\n')

        except Exception as e:
            print(f"An error occurred: {e}")

# Specify the host and port of your netcat listener
HOST = '83.136.253.251'  # The server's hostname or IP address
PORT = 51582        # The port used by the server

handle_netcat_connection(HOST, PORT) # connect to the netcat
```
<h3> The flag come out to be HTB{1_wiLl_sT0p_dR0p_4nD_r0Ll_mY_w4Y_oUt!}</h3>
