import firestore from '@react-native-firebase/firestore';

// ... inside your BookingScreen component ...

const handleConfirm = async () => {
  if (!date) {
    Alert.alert("Error", "Please enter a date.");
    return;
  }

  try {
    // This sends the data to your "Live" database
    await firestore().collection('Bookings').add({
      service: serviceTitle,
      requestedDate: date,
      instructions: notes,
      status: 'pending',
      createdAt: firestore.FieldValue.serverTimestamp(),
    });

    Alert.alert(
      "Success!", 
      "Your request is now live in the database!",
      [{ text: "Awesome", onPress: () => navigation.navigate('Profile') }]
    );
  } catch (error) {
    Alert.alert("Error", "Something went wrong with the connection.");
    console.error(error);
  }
};
