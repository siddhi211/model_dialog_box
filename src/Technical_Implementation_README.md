# Modal Component Implementation

2. ## Component Declaration
``` bash
const Modal = ({ isOpen, onClose, children }) => {
```
- `isOpen`: Boolean prop to control if the modal is visible.
- `onClose`: Function prop to close the modal.
- `children`: Content to display inside the modal.

3. ## Escape Key Handler
``` bash
useEffect(() => {
  const handleEscape = (event) => {
    if (event.key === 'Escape') {
      onClose();
    }
  };

  if (isOpen) {
    document.addEventListener('keydown', handleEscape);
  }

  return () => {
    document.removeEventListener('keydown', handleEscape);
  };
}, [isOpen, onClose]);
```

# Purpose: Allows the modal to close when the Escape key is pressed.

## How it works:

- When the modal is open (`isOpen` is true), a keydown event listener is added to the document
- The keydown event triggers whenever any keyboard key is pressed
- If the Escape key is detected, the `onClose` function is called
- The event listener is removed when either:
  - The modal closes
  - The component unmounts

4. ## Conditional Rendering
``` bash
if (!isOpen) return null;
```
- Purpose: If the modal is not open, render nothing (null).

5. ## Modal Markup
``` bash
return (
  <div className="modal-overlay" onClick={onClose}>
    <div className="modal-content" onClick={e => e.stopPropagation()}>
      {children}
    </div>
  </div>
);
```
- `modal-overlay`: Covers the whole screen. Clicking it triggers onClose to close the modal.
- `modal-content`: The actual modal box. Clicking inside it does not close the modal (e.stopPropagation() prevents the overlay's onClick from firing).
- `children`: Displays whatever is passed between <Modal>...</Modal> tags.

### APP.JS IMPLEMENTATION
# How the Button and Modal Are Tied Together

Visual Flow
User clicks "Open Modal" button
→ openModal() sets isModalOpen to true ( it renders the model component)
→ Modal appears.

User closes modal (by clicking "Close Modal", clicking outside, or pressing Escape)
→ closeModal() sets isModalOpen to false
→ Modal disappears.

