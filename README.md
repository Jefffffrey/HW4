<h1>HW4</h1>


```swift

import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Text("J'Select")
                .foregroundColor(.white)
                .font(.largeTitle)
                .fontWeight(.heavy)
                .foregroundStyle(.primary)
                .background(Image("Black"))
            TabView{
                Group{
                    WelcomeView()
                        .tabItem{
                            Image(systemName: "person.crop.circle")
                            Text("Welcome")
                        }
                    ShopListView()
                        .tabItem {
                            Image(systemName: "list.dash")
                            Text("Categories")
                        }
                    ItemView()
                        .tabItem {
                            Image(systemName: "link")
                            Text("items")
                        }
                }
                .toolbarBackground(Color.black, for: .tabBar)
                .toolbarBackground(.visible, for: .tabBar)
                .toolbarColorScheme(.dark, for: .tabBar)
            }
            .tint(.yellow)
        }
    }
}

import SwiftUI

struct WelcomeView: View {
    var body: some View {
        ZStack {
            Image("Bg2")
                .resizable()
                .aspectRatio(contentMode: .fill)
            Text("時時準備好")
                .offset(x:-120,y:-240)
                .fontWeight(.heavy)
                .font(.system(size: 16))
                .foregroundColor(.black)
            Text("裝扮 是讓我們每天能夠在")
                .offset(x:-50,y:-220)
                .fontWeight(.heavy)
                .font(.system(size: 16))
                .foregroundColor(.black)
            Text("真實世界裡生存下來的盔甲。")
                .offset(x:-10,y:-200)
                .fontWeight(.heavy)
                .font(.system(size: 16))
                .foregroundColor(.black)
            Text("-Bill Cunningham")
                .offset(x:100,y:-180)
                .fontWeight(.heavy)
                .font(.system(size: 16))
                .foregroundColor(.black)
        }
    }
}

import SwiftUI
struct Category : Identifiable {
    var id = UUID()
    var name : String 
    var image : String 
    var description : String
} 
var categories = [
    Category(name: "shoes", image: "Shoes", description: "鞋子"),
    Category(name: "clothes", image: "Clothes", description: "衣服"),
    Category(name: "pants", image: "Pants", description: "褲子"),
    Category(name: "accessories", image: "Accessories", description: "配件")
]

struct BasicImageRow : View {
    var thisCategory : Category
    var body: some View {
        HStack {
            Image(thisCategory.image)
                .resizable()
                .frame(width: 40, height: 40)
                .cornerRadius(5)
            Text(thisCategory.name)
        }
    }
}

struct CategoryDetailView : View {
    @Environment(\.presentationMode) var presentationMode 
    var thisCategory :Category
    var body: some View{
        ScrollView{
            VStack{
                Image(thisCategory.image)
                    .resizable()
                    .aspectRatio(contentMode: .fill)
                    .clipped()
                Text(thisCategory.name)
                    .font(.system(.title, design:.rounded))
                    .fontWeight(.black)
                Spacer()
                Text(thisCategory.description)
                    .font(.system(.subheadline, design:.rounded))
                    .fontWeight(.light)
                Spacer()
            }
        }
        .overlay(
            HStack{
                Spacer()
                VStack{
                    Button(action:{
                        self.presentationMode.wrappedValue.dismiss()
                    },label:{
                        Image(systemName:"chevron.down.circle.fill")
                            .font(.largeTitle)
                            .foregroundColor(.white)
                    })
                    .padding(.trailing, 20)
                    .padding(.top, 40)
                    Spacer()
                }
            }
        )
    }
}

struct ShopListView : View {
    @State var showDetailView = false
    @State var selectedCategory: Category?
    var body: some View{
                NavigationView{
            List(categories){
                categoryItem in BasicImageRow(thisCategory:categoryItem)
                    .onTapGesture{
                        self.showDetailView = true
                        self.selectedCategory = categoryItem
                    }
            }
                }
                .sheet(item: self.$selectedCategory){ thisCategory in CategoryDetailView(thisCategory: thisCategory)
                }
                .navigationBarTitle("分類項目")
    }
}

import SwiftUI

struct TermAndDescription: Identifiable{
    var id = UUID()
    var term:String
    var image:String
    var description:String
}
var myDictionary = [
    TermAndDescription(term: "DownJacket", image: "DownJacket",description: "$2480"),
    TermAndDescription(term: "Cardigan", image: "Cardigan",description: "$1380"),
    TermAndDescription(term: "Travis Scott x Nike SB Dunk Low PRO", image: "TAJ",description: "$66800"),
    TermAndDescription(term: "Sambas", image: "Sambas",description: "$2200")
    ,
    TermAndDescription(term: "Washedjean", image: "Washedjean",description: "$1580")
    ,
    TermAndDescription(term: "Jean", image: "Jean",description: "$1280")
    ,
    TermAndDescription(term: "Airpods Pro Max", image: "AirPods",description: "$23800")
    ,
    TermAndDescription(term: "Sunglasses", image: "Sunglasses",description: "$2380")
]

struct ItemView: View{
    @State var currentCard = 0
    var body: some View{
        VStack{
            VStack{
                Text(myDictionary[currentCard].term)
                    .font(.title)
                    .padding(.all, 10)
                Image((myDictionary[currentCard].image))
                    .resizable()
                    .aspectRatio(contentMode: .fill)
                    .frame(width:300,height:300)
                    .cornerRadius(15)
                    .overlay{
                        RoundedRectangle(cornerRadius: 20)
                            .stroke(Color.brown, lineWidth: 4)
                    }
                Text(myDictionary[currentCard].description)
                    .font(.body)
                    .foregroundColor(.gray)
                    .padding(.all, 10)
            }
            //.frame(minWidth: 0, idealWidth: 100, maxWidth: 300, minHeight: 0, idealHeight: 100, maxHeight: 300, alignment: .center)
                        //.background(Color.yellow)
            .onTapGesture{
                if currentCard<myDictionary.count-1{
                    currentCard+=1
                }else{
                    currentCard=0
                }
            }
            Text("點擊查看下一張")
                .padding(.all, 10)
        }
    }
}


```
https://github.com/Jefffffrey/HW4#:~:text=rename%20HW4%20to%20HW4.md-,img_0247.mov,-Add%20files%20via
