# 8
float mutationRate = 0.01;
int totalPopulation = 150;

DNA[] population;
ArrayList<DNA>matingPool;
String target;

PFont f;

void setup(){
  size(1920,1080);
  target = "to be or not to be";
  
  population = new DNA[totalPopulation];
  for(int i=0;i<population.length;i++){
    population[i] = new DNA(target.length());
  }
  
  f = createFont("Courier New",12,true);
}

void draw(){
  
  for(int i=0;i<population.length;i++){
    population[i].calcFitness(target);
  }
  
  ArrayList<DNA>matingPool = new ArrayList<DNA>();
  
  for(int i=0;i<population.length;i++){
    int nnnn = int(population[i].fitness*100);
    for(int j=0;j<nnnn;j++){
      matingPool.add(population[i]);
    }
  }
  for(int i=0;i<population.length;i++){    
    int a = int(random(matingPool.size()));
    int b = int(random(matingPool.size()));
    DNA partnerA = matingPool.get(a);
    DNA partnerB = matingPool.get(b);    
    
    DNA child = partnerA.crossover(partnerB);
    
    child.mutate(mutationRate);
    
    population[i] = child;
    }
    background(255);
    fill(0);
    String everything = "";
    for(int i=0;i<population.length;i++){
      everything += population[i].getPhrase()+"    ";
    }
    textFont(f,12);
    text(everything,10,10,width,height);
  }
