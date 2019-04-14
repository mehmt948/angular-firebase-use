##Angular Firebase Usage
###1 - Project Settings and imports
######environment.ts
     production: false,
       firebase: 
       //these options is unique and you can get from firebase site
       {
                apiKey: "",
                authDomain: "",
                databaseURL: "",
                projectId: "",
                storageBucket: "",
                messagingSenderId: ""
       }
       //when creating new firebase project you can get these options for angular
       
######app.module.ts
    import { environment } from '../environments/environment';
    import { AngularFireModule } from '@angular/fire';
    import { AngularFirestoreModule } from '@angular/fire/firestore';
    import { AngularFireStorageModule } from '@angular/fire/storage';
    import { AngularFireAuthModule } from '@angular/fire/auth';
    
    imports: [
        BrowserModule,
        AngularFireModule.initializeApp(environment.firebase),
        AngularFirestoreModule, // imports firebase/firestore, only needed for database features
        AngularFireAuthModule, // imports firebase/auth, only needed for auth features,
        AngularFireStorageModule // imports firebase/storage only needed for storage features
      ],
       
######app.component.ts
    import { AngularFirestore } from '@angular/fire/firestore';
    constructor(private db: AngularFirestore) {}
###2- Queries
####1 - Getting all documents
    this.db.collection('users').get().subscribe(querySnapshot => {
      querySnapshot.forEach(doc => {
        console.log(doc.id, " => ", doc.data());
      });
    }); 
####2 - Add document to collection
    //Basic data adding document adding
    //if document exits it will overwrite it 
    //else it will create new document with id of new-city-id
    this.db.collection("cities").doc("new-city-id").set(data);
    
    // Add a new document with a generated id.
    this.db.collection("cities").add({
        name: "Tokyo",
        country: "Japan"
    })
    .subscribe(docRef => {
        console.log("Document written with ID: ", docRef.id);
    });
####3 - Deleting or adding new data to doc
    const docRef = this.db.collection('users').doc(DOCID).set({
      {newDataObject}    
    );
####4 - Find spesific documents
    this.db.collection('cities').where('capital', '==', 'course1')
    .get(querySnapshot => {
      querySnapshot.forEach(doc => {
        console.log(doc.id, ' => ', doc.data());
      })
    })
###Possible Data Types
    var docData = {
        stringExample: "Hello world!",
        booleanExample: true,
        numberExample: 3.14159265,
        dateExample: firebase.firestore.Timestamp.fromDate(new Date("December 10, 1815")),
        arrayExample: [5, true, "hello"],
        nullExample: null,
        objectExample: {
            a: 5,
            b: {
                nested: "foo"
            }
        }
    };
    this.db.collection("users").doc("one").set(docData).subscribe(()=>{
        console.log("Document successfully written!");
    });
