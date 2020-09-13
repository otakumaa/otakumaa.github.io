---
layout: post
title:      "My First CLI project"
date:       2020-09-13 01:38:28 +0000
permalink:  my_first_cli_project
---


So my first CLI was an extremely daunting task in my head, it took me a while to figure out what i even wanted my project topic to be.I  then figured why not try pokemon if its supposed to be supposed to be "something I could fill a room talking about ". So I went to my computer and looked up Pokemon API and found POKEAPI which is very organized and has everything from moves, versions, abilities and types. So then starts my journey on my very own CLI project which had many ups and downs which i will share with you.

Alright so my first hurdle was figuring out how to even start making this, i watched a video of Avi making a Ruby Gem so i decided to take that route, which led to many google searches on how to make gems and i found the easiest way was to use bundler since it would populate all of the files i needed to start with.

my second hurdle was not necessarily coding related but did shave two days off of my working time, the fires all around california lead to my power being shut off for two whole days and then needing to evacuate which was an entire ordeal. but after I arrived at my cousins house it was time to set my computer back up and get to work since i had lost much valuable time. 


I was on a roll i wanted all the data i could pull from my API and make a robust CLI application but unfortunately reality hit me harder than expected and i knew i didnt have the time so given that I had lost two days ( and still work full time)  so i am now settling for making a working CLI that will get me past this first project. so i am creating a simple pokedex that when you enter what pokemon you are looking for will return their type, abilities and moves. 


For me figuring out how to retrieve the data from the API and using was the most dificult thing to understand. although we had gone over it a bit i had to do a lot of searching in order to figure it out. I found examples that helped me refactor it to make it look much better.

```

class API
    def self.get_names
       response = RestClient.get("https://pokeapi.co/api/v2/pokemon?limit=700")
       pokemon_array = JSON.parse(response.body)["results"]
       pokemon_array.each do |poke|
          Pokemon.new(poke["name"])
        end   
    end
    def self.get_details(pokemon)
       response = RestClient.get("https://pokeapi.co/api/v2/pokemon/#{pokemon}")
       poke = Pokemon.find_by_name(pokemon)[0]
       moves_array = JSON.parse(response.body)["moves"].map do |move|
          move["move"]["name"]
       end 
       abilities_array = JSON.parse(response.body)["abilities"].map do |ability|
          ability["ability"]["name"]
       end 
       poke.type = JSON.parse(response.body)["types"][0]["type"]["name"]
       poke.moves = moves_array.join("\n")
       poke.ability = abilities_array.join("\n") 
       poke
    end 
 end 
```

Creating the actual CLI was pretty fun and i do wish i had more time to make my application more robust. the way it is now doesnt necessarily present it in the best ways possible. i am definitely going come back to this when i have free time because i have so many ideas to make it better.




