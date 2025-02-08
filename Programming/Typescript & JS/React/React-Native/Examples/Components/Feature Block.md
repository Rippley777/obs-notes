```javascript
const FeatureBlock = ({ icon, title, description }) => {
  return (
    <View style={styles.featureBlock}>
      <Image source={icon} style={styles.featureIcon} />
      <Text style={styles.featureTitle}>{title}</Text>
      <Text style={styles.featureDescription}>{description}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  featureBlock: {
    alignItems: 'center',
    padding: 20
  },
  featureIcon: {
    width: 50,
    height: 50,
    marginBottom: 10
  },
  featureTitle: {
    color: '#fff',
    fontSize: 16,
    fontWeight: 'bold'
  },
  featureDescription: {
    color: '#fff',
    textAlign: 'center'
  }
});

```