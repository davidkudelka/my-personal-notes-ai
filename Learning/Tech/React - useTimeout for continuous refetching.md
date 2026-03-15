  * tags: #refetch #timeout #javascript #react
  * notes:
    * ```typescript
const Componnet = () => {
  const savedCallback = useRef<null | NodeJS.Timeout>(null)

  useEffect(() => {
    // If not expanded cancel refetching
    if(!isExpanded) {
      return savedCallback.current && 
      clearTimeout(savedCallback.current)
    }

    // SetTimeout recursion
    function createTimeout() {
      return setTimeout(() => {
        refetch({}, {fetchPolicy: 'store-and-network'});
        savedCallback.current = createTimeout()

      }, TWO_MINUTES)
    }

    // Starting the cycle
    savedCallback.current = createTimeout()

    // ON un-mount you want to clear timeout
    return () => {
      savedCallback.current && 
      clearTimeout(savedCallback.current)
    }
  })


  return <div /> 
}```