```javascript
const Footer = () => {
  return (
    <View style={styles.footer}>
      <Text style={styles.footerText}>© 2024 TrackRabbit LLC</Text>
      {/* Add icons if needed */}
    </View>
  );
};

const styles = StyleSheet.create({
  footer: {
    padding: 20,
    alignItems: 'center'
  },
  footerText: {
    color: '#fff'
  }
});

```