<template>
  <q-layout>
    <q-page-container>
      <q-page>             
        <q-card>
          <q-card-section class="bg-deep-purple-11">   
            <q-select
              outlined  
              bg-color="deep-purple-1"            
              :value="search"
              @input="setSelected"
              use-input
              hide-selected
              fill-input          
              :options="options"
              @filter="filterFn"              
              @input-value="setModel"
              :hint="hint"                                
            >              
            </q-select>                               
          </q-card-section>
          <q-card-section class="bg-red-1">            
            <div class="text-h6">{{ courseTitle }}</div>
            <div v-if="courseTitle">
              <div class="q-pt-sm">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore
                magna aliqua. Vulputate odio ut enim blandit volutpat. Nisi scelerisque eu ultrices vitae auctor eu augue ut. 
                Leo in vitae turpis massa. Aenean et tortor at risus viverra adipiscing at. Eu tincidunt tortor aliquam nulla. 
                Nunc sed velit dignissim sodales ut eu sem integer vitae. Convallis aenean et tortor at.
              </div>     
              <div class="q-pt-sm text-bold">
                Prerequisities: MTH 101, CS 150
              </div>                
              <div class="q-pt-sm text-bold">
                Proctored Exams: Yes
              </div>                
              <div class="q-pt-sm text-bold">
                Group Work: N/A
              </div>   
              <div class="q-pt-sm text-bold">
                Terms Available: Spring, Fall
              </div>                     
            </div>
            <div v-else>No course selected</div> 
          </q-card-section>
          <q-card-section class="bg-green-1">            
            <q-tabs
              v-model="tab"
              dense
              class="text-grey"
              active-color="primary"
              indicator-color="primary"
              align="justify"
              narrow-indicator
            >
              <q-tab name="stats" label="Stats" />
              <q-tab name="reviews" label="Reviews" />
            </q-tabs>
            <q-tab-panels v-model="tab" animated>
              <q-tab-panel name="stats">
                <div class="text-h6">Stats</div>
                 <q-knob
                    readonly
                    v-model="knobValue"
                    show-value
                    size="90px"
                    :thickness="0.22"
                    color="orange"
                    track-color="orange-3"
                    class="text-orange q-ma-md"
                  />
                  <q-knob
                    readonly
                    v-model="knobValue2"
                    show-value
                    size="90px"
                    :thickness="0.22"
                    color="green"
                    track-color="yellow-5"
                    class="text-orange q-ma-md"
                  />
              </q-tab-panel>

              <q-tab-panel name="reviews">
                <div class="text-h6">Reviews</div>
                <div v-for="review in reviews" :key="review.reviewDate" class="q-mb-md">
                  <div>Reviewed by {{ review.username }} on {{ review.reviewDate }}</div>
                  <div>
                    Difficulty
                    <q-icon v-for="n in review.difficulty" name="star" class="text-orange" />            
                  </div>   
                  <div class="stars">
                    Usefulness
                    <q-icon v-for="n in review.usefulness" name="star" class="text-orange"/>            
                  </div>                   
                  <div>Instructor: {{ review.instructor }}</div>
                  <div>Year Taken: {{ review.yearTaken }}</div>   
                  The virus is mainly spread between people during close contact, often via small droplets produced during 
                  coughing, sneezing, or talking. While these droplets are produced when breathing out, they usually fall 
                  to the ground or surfaces rather than being infectious over large distances. People may also become infected 
                  by touching a contaminated surface and then their face. The virus can survive on surfaces for up to 72 hours. 
                  Coronavirus is most contagious during the first three days after onset of symptoms, although spread may be 
                  possible before symptoms appear and in later stages of the disease.   
                  <hr>          
                </div>                              
              </q-tab-panel>
            </q-tab-panels>
          </q-card-section>
        </q-card>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script>
const courses = ['CS 161 - Intro to Computer Science I', 'CS 225 - Data Structures', 'CS 325 - Analysis of Algorithms', 'CS 361 - Software Engineering I']

export default {
  name: 'MainLayout',
  data () {
    return {
      search: '',
      hint: 'Find a course',
      options: [],
      courseTitle: '',
      tab: '',
      knobValue: 77,
      knobValue2: 92,
      reviews: [
        {
          username: 'David',
          yearTaken: 2030,
          reviewDate: '2020-01-15',
          instructor: 'Bradbury, R.',          
          difficulty: 4,
          usefulness: 4
        },
        {
          username: 'Taka',
          yearTaken: 2025,
          reviewDate: '1850-05-22',
          instructor: 'Einstein, A.',         
          difficulty: 5,
          usefulness: 5
        },
        {
          username: 'Martin',
          yearTaken: 2012,
          reviewDate: '1984-06-08',
          instructor: 'Vonnegut, K.',          
          difficulty: 2,
          usefulness: 4
        }
      ]
    }
  },
  methods: {
    filterFn(val, update, abort) {
      update(() => {
        const needle = val.toLocaleLowerCase()
        this.options = courses.filter(v => v.toLocaleLowerCase().indexOf(needle) > -1)
      })
    },
    setModel(val) {
      this.search = val
    },
    setSelected() {
      this.courseTitle = this.search
    }
  },
  computed: {
    elasticOptions() {

    }
  }
}
</script>