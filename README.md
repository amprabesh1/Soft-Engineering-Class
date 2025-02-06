import kivy
from kivy.app import App
from kivy.uix.label import Label
from kivy.uix.button import Button
from kivy.uix.textinput import TextInput
from kivy.uix.boxlayout import BoxLayout

class TobaccoSurvey(App):
    
    def build(self):
        # Creating the layout
        layout = BoxLayout(orientation='vertical', padding=10)
        
        # Creating the labels
        label1 = Label(text='How old are you?')
        label2 = Label(text='Which brands of tobacco do you use?')
        label3 = Label(text='How frequently do you use tobacco?')
        
        # Creating the inputs
        self.age_input = TextInput(multiline=False, input_type='number')
        self.type_input = TextInput(multiline=False)
        self.frequency_input = TextInput(multiline=False)
        
        # Creating the buttons
        submit_button = Button(text='Submit', on_press=self.submit)
        clear_button = Button(text='Clear', on_press=self.clear)
        info_button = Button(text='Info', on_press=self.show_info)
        
        # Including widgets in the design
        layout.add_widget(label1)
        layout.add_widget(self.age_input)
        layout.add_widget(label2)
        layout.add_widget(self.type_input)
        layout.add_widget(label3)
        layout.add_widget(self.frequency_input)
        layout.add_widget(submit_button)
        layout.add_widget(clear_button)
        layout.add_widget(info_button)
        
        return layout
    
    def submit(self, instance):
       #Obtaining values from inputs
        age = int(self.age_input.text)
        tobacco_type = self.type_input.text
        frequency = self.frequency_input.text
        
        if age < 21:
            #letting the user know they're too young
            message = 'Sorry, you must be 21 years or older to purchase tobacco products.'
        else:
            # Congratulating the user for finishing the survey.
            message = 'We appreciate you completing the survey!'
            # Taking action with the survey data, like putting it in a database.
            
        # Showing the message.
        self.display_message(message)
    
    def clear(self, instance):
       # Eliminating fields in the inputs
        self.age_input.text = ''
        self.type_input.text = ''
        self.frequency_input.text = ''
    
    def display_message(self, message):
        # Making a label to put the message on.
        message_label = Label(text=message)
        self.root.add_widget(message_label)
        
    def show_info(self, instance):
        # Presenting some facts regarding tobacco products.
        message = 'Kill your cigarettes and tobaccos, or they will kill you'
        self.display_message(message)
    
if __name__ == '__main__':
    TobaccoSurvey().run()
