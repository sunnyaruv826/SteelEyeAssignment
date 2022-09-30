# SteelEyeAssignment

# Ans_1
List component is displaying a list of text as SingleListItem. It takes an array of objects with each object mandatorily having text as its key. SingleListItem is showing the text and upon clicking it that particular list item will become green while the other options turns red. To determine which list item is selected; WrappedListComponent state contains a state named `selectedIndex`, it contains the index of item which is currently selected by the user.


# Ans_2
1. Uncaught TypeError: prop_types_WEBPACK_IMPORTED_MODULE_2__default(...).shapeOf is not a function
2. factoryWithTypeCheckers.js:183 Uncaught Invariant Violation: Calling PropTypes validators directly is not supported by the `prop-types` package. Use `PropTypes.checkPropTypes()` to call them.
3. Uncaught TypeError: Cannot read properties of null (reading 'map')
4. The above error occurred in the <WrappedListComponent> component:
at WrappedListComponent  
5. Warning: Each child in a list should have a unique "key" prop.
6. react-dom.development.js:86 Warning: Failed prop type: Invalid prop `isSelected` of type `function` supplied to `WrappedSingleListItem`, expected `boolean
7. Uncaught TypeError: setSelectedIndex is not a function.

  
  # Ans_3
  import React, { useState, useEffect, memo,useRef } from 'react';
import PropTypes from 'prop-types';

// Single List Item
const WrappedSingleListItem = ({
  index,
  isSelected,
  onClickHandler,
  text,
}) => {
  
  return (
    <li
      style={{ backgroundColor: isSelected ? 'green' : 'red'}}
      onClick={()=>onClickHandler(index)}
    >
      {text}
    </li>
  );
};

WrappedSingleListItem.propTypes = {
  index: PropTypes.number.isRequired,
  isSelected: PropTypes.bool.isRequired,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};

const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({
  items,
}) => {
  const [selectedIndex, setSelectedIndex] = useState();

  useEffect(() => {
    setSelectedIndex(null);
  }, [items]);

  const handleClick = useRef(index => {
    setSelectedIndex(index);
  });
  

  return (
    <ul style={{ textAlign: 'left' }}>
      {items?.map((item, index) => (
        <SingleListItem
          onClickHandler={ handleClick.current}
          key={item.id}
          text={item.text}
          index={index}
          isSelected={selectedIndex === index} 
        />
      ))}
    </ul>
  )
};

WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(PropTypes.shape({
    text: PropTypes.string.isRequired,
    id: PropTypes.string.
  })),
};

WrappedListComponent.defaultProps = {
  items: [{
    id:"1",
    text:"steel"

  },{
    id:"2",
    text:"eye"

  },
  {
    id:"3",
    text:"ear"

  },
  {
    id:"4",
    text:"iron"

  },
  
  

],
};

const List = memo(WrappedListComponent);

export default List;
   
  
