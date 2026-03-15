  * tags: #article #react #suspense #concurrency #throttling
  * link to article: https://andreigatej.dev/blog/on-react-suspense-throttling/
  * author: [[Andrei Gatej]]
  * notes:
    * ### React suspense
      * React suspense have small delay before triggering suspense fallback, in case your request would come in very short time before falling into fallback
      * It's performance optimisation, so we can avoid too many re-renders for fast response's
