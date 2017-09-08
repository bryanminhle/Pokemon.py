# Pokemon.py

'''
    File: pokemon.py
    Author: Bryan Le
    Purpose: Organizes data in a .csv file using a 2d dictionary and returns
         the highest average query to the user.
    Class: CSC 120, Section 001F, FA17
'''

def pokemon_catalog():
    """Reads in a .csv file and turns its data into a 2d list.
      
        Parameters: none
      
        Returns: A 2d list to allow accessibility to each element.
      
        Pre-condition: File.
      
        Post-condition: The return value is a 2d list."""  
     
    file = input()
    open_file = open(file)
    read = open_file.readlines()
    csv_file = []
    for i in read: # creates the 2d list from .csv file
        row = i.split(',')
        csv_file.append(row)
    del csv_file[0] # deletes first row of .csv file
    return csv_file

def dict_1(pokemon_lists):
    """Create a dictionary with Pokemon names mapped to their attributes.
      
        Parameters: 2d list cataglog of pokemon.
      
        Returns: A dictionary where the pokemon name is mapped to the integer
            values of their attributes.
      
        Pre-condition: 2d list.
      
        Post-condition: The return value is a 2d dictionary."""    
    name_to_attributes = {}
    attributes = []
    index = 0 #while-loop index
    while index < len(pokemon_lists): # creates list of attributes for each pokemon
        attributes.append(pokemon_lists[index][2, 4:10])    
        index += 1

    for i in range(0, len(attributes)): # turns string of numbers into integers
        for j in range(0, len(attributes[i])):
            attributes[i][j] = int(attributes[i][j])        
    
    for i in range(0, len(pokemon_lists)): # sets each pokemon name mapped to their attributes
        name_to_attributes[ pokemon_lists[i][1] ] = attributes[i]
    print(name_to_attributes)
    return name_to_attributes

def dict_2(in_dict, pokemon_lists):
    """Creates a 2d dictonary using catalog of pokemon and previously 
        made dictionary.
      
        Parameters: in_dict is a dictionary and pokemon_lists is 2d list catalog of pokemon.
        
        Returns: A 2d dictionary with types of pokemon mapped to the name of the pokemon.
      
        Pre-condition: Dictionary and 2d list.
      
        Post-condition: The return value is a 2d dictionary."""    
    pokemon_dict = {}
    types = []
    for i in pokemon_lists: # creates list of each type of pokemon
        if i[2] not in types:
            types.append(i[2])
    for i in range(0, len(types)): # creates a list for each type of pokemon
        types[i] = []
        
    for i in range(0, len(pokemon_lists)): # appeneds pokemon name to their list type
        if pokemon_lists[i][2] == types[i]:
            types[i].append(pokemon_lists[i][1])
            
        
    #for i in pokemon_lists:
            #for name in in_dict.keys():
            #    if i[2] in types:
            #        #if name in i:
                 #   pokemon_dict[ i[2] ] = name
                 
def main():
    file = pokemon_catalog()
    inner_dict = dict_1(file)
    outter_dict = dict_2(inner_dict, file)
    
main()
