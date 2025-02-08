```javascript
import React from 'react';
import { View, Text, ImageBackground, StyleSheet, TouchableOpacity } from 'react-native';

const HeroSection = () => {
  return (
    <ImageBackground source={require('./path-to-hero-bg.jpg')} style={styles.hero}>
      <Text style={styles.heroText}>UPLOAD AND SHARE YOUR MUSIC PRIVATELY</Text>
      <TouchableOpacity style={styles.button}>
        <Text style={styles.buttonText}>Get Started</Text>
      </TouchableOpacity>
    </ImageBackground>
  );
};

const styles = StyleSheet.create({
  hero: {
    height: 300,
    justifyContent: 'center',
    alignItems: 'center'
  },
  heroText: {
    color: '#fff',
    fontSize: 18,
    textAlign: 'center',
    marginHorizontal: 20,
    marginBottom: 20
  },
  button: {
    backgroundColor: 'red',
    paddingVertical: 10,
    paddingHorizontal: 30,
    borderRadius: 5
  },
  buttonText: {
    color: '#fff'
  }
});

```