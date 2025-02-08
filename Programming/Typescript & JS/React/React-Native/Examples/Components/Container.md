```javascript
import React from 'react';
import { ScrollView, StyleSheet, View } from 'react-native';
import HeroSection from './HeroSection';
import FeatureBlock from './FeatureBlock';
import Footer from './Footer';

const App = () => {
  return (
    <ScrollView style={styles.container}>
      <HeroSection />
      <FeatureBlock icon={require('./path-to-create-icon.png')} title="CREATE" description="Create albums and tracks for sharing." />
      <FeatureBlock icon={require('./path-to-upload-icon.png')} title="UPLOAD" description="Upload audio and cover art for the albums and tracks you create." />
      <FeatureBlock icon={require('./path-to-share-icon.png')} title="SHARE" description="Instantly create unique links to share privately with other people." />
      <Footer />
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#000'
  }
});

export default App;

```