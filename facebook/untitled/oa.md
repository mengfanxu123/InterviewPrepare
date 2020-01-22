# OA





```text
Input:
numToys = 6
topToys = 2
toys = ["elmo", "elsa", "legos", "drone", "tablet", "warcraft"]
numQuotes = 6
quotes = [
"Elmo is the hottest of the season! Elmo will be on every kid's wishlist!",
"The new Elmo dolls are super high quality",
"Expect the Elsa dolls to be very popular this year, Elsa!",
"Elsa and Elmo are the toys I'll be buying for my kids, Elsa is good",
"For parents of older kids, look into buying them a drone",
"Warcraft is slowly rising in popularity ahead of the holiday season"
];

Output:
["elmo", "elsa"]

Explanation:
elmo - 4
elsa - 4
"elmo" should be placed before "elsa" in the result because "elmo" appears in 3 different quotes and "elsa" appears in 2 different quotes.
```

```java
class State{
    
    HashSet<Integer> set;
    int freq;
    String name;
    
    public State(String name){
        this.name = name;
        freq = 0;
        set = new HashSet();
    }
    
}

public class Main {
    
    public static void main(String[] args) {
        
        int numToys = 6;
        int topToys = 2;
        ArrayList<String> toys = new ArrayList(Arrays.asList("elmo", "elsa", "legos", 
                                                             "drone", "tablet", "warcraft"));
        int numQuotes = 6;
        ArrayList<String> quotes = new ArrayList(Arrays.asList(
            "Elmo is the hottest of the season! Elmo will be on every kid's wishlist!",
            "The new Elmo dolls are super high quality",
            "Expect the Elsa dolls to be very popular this year, Elsa!",
            "Elsa and Elmo are the toys I'll be buying for my kids, Elsa is good",
            "For parents of older kids, look into buying them a drone",
            "Warcraft is slowly rising in popularity ahead of the holiday season"
        ));
        
        HashMap<String, State> map = new HashMap();
        
        for( int i = 0; i < toys.size(); i++ ){
            
            String key = toys.get( i ).toLowerCase();
            
            map.put( key , new State(key) );
        }
        
        for( int i = 0; i < quotes.size(); i++ ){
            String[] x = quotes.get( i ).split("[,! ]");
            
            for( int j = 0; j < x.length; j++ ){
                String key = x[j].toLowerCase();
                
                if( map.containsKey( key ) ) {          
                    State state = map.get( key );    
                    state.freq++;
                    state.set.add( i );     
                    map.put( key, state );
                }
            }
            
        }
        
        PriorityQueue<State> pq = new PriorityQueue<>( ( x, y ) -> {
            
            if( x.freq == y.freq ) return y.set.size() - x.set.size();
            return x.freq - y.freq;
            
        } );
        
        for( Map.Entry< String, State > entry: map.entrySet() ){
            pq.add( entry.getValue() );
            if( pq.size() > topToys ) pq.poll();
        }
        
        while( pq.size() != 0 ) { 
            State state = pq.poll();
            System.out.println( state.name + "->" + state.freq );
        }
        
    }
}
```



