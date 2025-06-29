---------------
Denji's Taxi Job
---------------

This is a pretty straightforward job script for QBCore that lets your players pick up passengers, drive them around, and get paid.

The fun part is the dialogue system—clients will ask you questions during the trip, and how you answer affects your rating and your final tip.

---------------
Features
---------------

- Go On Duty: Start your shift at an NPC and get a taxi provided.
- Random Fares: Get calls for pickups and drop-offs all over the map.
- Interactive Dialogue: Clients will talk to you and ask questions with voice lines.
- 5-Star Rating System: Start with a 3-star rating. Answering questions nicely can raise it, while being rude will lower it.
- Tip System: A higher star rating at the end of a fare means a bigger tip!
- Customizable: Almost everything can be easily changed in the `config.lua`.

---------------
Dependencies
---------------

This script was built to work with these resources. Make sure you have them started.

- `qb-core`
- `ox_lib`
- `ox_target`
(Recommended) - `Renewed-Banking` (can be swapped for another banking script with a quick change in `server/sv_main.lua`)
- A key script like `qb-vehiclekeys`

---------------
Installation
---------------

1. Drag the `denji-taxi` folder into your `resources` directory.
2. Add `ensure denji-taxi` to your `server.cfg` file. Make sure you start it *after* all of the dependencies listed above.
3. Restart your server. You're good to go!

---------------
Audio Setup
---------------

This script uses voice lines for the dialogue system. You can change audio files to match your language.

1. Place your `.ogg` audio files in the `html/audio/` folder.
2. The script finds voice lines based on the passenger's gender. The naming is important:

   - `filename_male.ogg`
   - `filename_female.ogg`

For example, in `config.lua`, if you have a dialogue entry with `audio = "q_busy_day"`, the script will look for `q_busy_day_male.ogg` and `q_busy_day_female.ogg`.

---------------
Configuration
---------------

You can change most things in the `config.lua` file.

**Passenger Models**

You need to tell the script which character models to use for male and female passengers. This is how it knows which voice line folder to use.

Config.MalePassengerModels = { 's_m_y_passenger_01', 's_m_y_tourist_01', 'a_m_y_hipster_01', 'a_m_y_business_01' }
Config.FemalePassengerModels = { 's_f_y_tourist_01', 'a_f_y_tourist_01', 'a_f_y_hipster_01', 'a_f_y_business_02' }

**Dialogue & Rating**

This is where you write the conversations.

- `question` is what the NPC says.
- `audio` is the filename for the voice line (without `_male.ogg` or `_female.ogg`).
- `answers` is a list of up to 3 responses for the player.
- Add `good = true` to an answer to make it increase the player's rating.
- Add `bad = true` to an answer to make it lower the player's rating.

Config.Dialogue = {
    {
        question = "So, busy day for you?",
        audio = "q_busy_day",
        answers = {
            { text = "Just the way I like it.", good = true },
            { text = "It's alright." },
            { text = "Can we just drive?", bad = true },
        }
    },
    -- ... more questions here ...
}

**Keybinds**

The default keys are `J` to accept a fare, and `U`, `I`, `O` for dialogue answers. Your players can change these in their `FiveM Settings > Key Bindings > Denji's Taxi Job` menu.
