- // Import the necessary libraries
import React, { Component } from 'react';
import { StyleSheet, Text, View, TextInput, Button } from 'react-native';

// Define the App component
class App extends Component {

  // State variables
  state = {
    name: '',
    email: '',
    message: ''
  };

  // Handle the submit button press
  handleSubmit = () => {
    // Send the form data to the server
    fetch('https://example.com/api/womens-parliament', {
      method: 'POST',
      body: JSON.stringify({
        name: this.state.name,
        email: this.state.email,
        message: this.state.message
      }),
      headers: {
        'Content-Type': 'application/json'
      }
    })
      .then(response => response.json())
      .then(data => {
        if (data.success) {
          // Success!
          alert('Your message has been sent.');
        } else {
          // Error!
          alert('There was an error sending your message.');
        }
      });
  };

  // Render the UI
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.title}>Women's Parliament</Text>
        <TextInput
          style={styles.input}
          placeholder="Your name"
          onChangeText={(text) => this.setState({ name: text })}
        />
        <TextInput
          style={styles.input}
          placeholder="Your email"
          onChangeText={(text) => this.setState({ email: text })}
        />
        <TextInput
          style={styles.input}
          placeholder="Your message"
          multiline
          onChangeText={(text) => this.setState({ message: text })}
        />
        <Button
          title="Submit"
          onPress={this.handleSubmit}
        />
      </View>
    );
  }
}

// Define the styles
const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center'
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold'
  },
  input: {
    height: 40,
    borderColor: '#ccc',
    borderWidth: 1,
    padding: 10
  }
});

// Export the App component
export default App;
